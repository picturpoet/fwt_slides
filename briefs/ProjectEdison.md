# **AI Decision Making System**

Product Requirements Document  
Version 1.0 | December 2025

# **1\. Executive Summary**

This platform provides AI-driven order routing, intelligent fulfillment location selection, and predictive inventory optimization for Fantasy World Toys' delivery operations across one central warehouse and five micro-fulfillment centers (MFCs) in Kuwait. The system ingests orders from Magento e-commerce and mobile applications, applies multi-factor scoring algorithms to determine optimal fulfillment strategy, and outputs decisions to the downstream Delivery Admin Platform for execution.

## **Business Context**

The platform supports a toy retail operation handling 100-150 daily orders with three delivery tiers: Normal (\<3 hours), Express (\~2 hours), and Super Express/Quick Commerce (\<1 hour). Current fulfillment relies on manual location assignment, resulting in suboptimal routing, excessive store pull-outs, and inconsistent delivery times. This system introduces algorithmic decision-making with human oversight to reduce store disruption by 40% and improve delivery times by 25-40%.

# **2\. System Context**

## **System Architecture Overview**

| System | Role & Integration |
| :<hr class="my-8 border-t border-gray-300">- | :<hr class="my-8 border-t border-gray-300">- |
| **Magento 2.4.8** | E-commerce order source. Sends orders via webhooks to this platform. Receives fulfillment location assignment and status updates. |
| **Customer App** | Mobile order source. Orders flow via API to this platform for routing decisions. |
| **Dynamics AX 2012** | ERP system providing real-time inventory data and POS transaction history. APIs to be built by FWT in-house team. |
| **Google Maps API** | Distance matrix and route optimization. Provides travel time estimates for scoring algorithm. |
| **AI Decision Making System (this PRD)** | Core intelligence layer. Receives orders, applies scoring algorithm, selects fulfillment location, optimizes routes, outputs decisions. Orchestrated via n8n on Azure. |
| **Delivery Admin Platform** | Downstream system. Receives routed tasks from this platform for dispatcher assignment and driver execution. |
| **Driver App** | .NET/Mobile application. Receives route and order details from Delivery Admin Platform. |

**Data Flow:** Magento/Customer App → AI Decision Making System → Delivery Admin Platform → Driver App

# **3\. Phase 1 Scope (MVP)**

Phase 1 delivers core order routing capability: receive orders, apply scoring algorithm, select optimal fulfillment location, optimize delivery routes, and output decisions to downstream systems. Initial deployment covers Warehouse (999) and Al Rai MFC (101). Target: operational readiness within 60 days of development start.

## **3.1 Order Ingestion**

**Functional Requirements**

1. **Magento Webhook Integration**  
* RESTful endpoint to receive order events from Magento 2.4.8  
* Order payload: order ID, line items with SKUs, delivery address, customer contact, delivery type (Normal/Express/Super Express), time window  
* Idempotent processing to handle duplicate webhook deliveries  
2. **Customer App API Integration**  
* API endpoint for mobile application order submission  
* Same payload structure as Magento for consistency  
3. **Order Parsing Engine**  
* Normalize incoming orders into internal data model  
* Validate required fields and flag incomplete orders for manual review  
* Extract delivery priority from order metadata

## **3.2 AI Order Routing**

**Functional Requirements**

1. **Scoring Algorithm**  
* Multi-factor weighted scoring to rank fulfillment locations per order  
* Scoring factors: inventory availability, distance to customer, location capacity, delivery priority weighting  
* Configurable weight parameters per factor  
2. **Inventory Check Module**  
* Real-time inventory query against Dynamics AX 2012 via API  
* SKU-level availability check across all enabled fulfillment locations  
* Support for partial fulfillment detection (order splitting candidate)  
3. **Distance Calculation Module**  
* Google Maps Distance Matrix API integration  
* Calculate travel time from each fulfillment location to delivery address  
* Factor in real-time traffic conditions  
4. **Capacity Assessment Module**  
* Track current order load per fulfillment location  
* Configurable capacity thresholds per location  
* Deprioritize overloaded locations in scoring  
5. **Priority Weighting System**  
* Super Express orders: maximize proximity, minimize fulfillment time  
* Express orders: balance proximity with inventory depth  
* Normal orders: optimize for operational efficiency and store disruption reduction

## **3.3 Order Processing**

**Functional Requirements**

1. **Location Selection Logic**  
* Select highest-scoring fulfillment location from algorithm output  
* Fallback to secondary location if primary unavailable  
* Flag orders with no viable fulfillment option for manual intervention  
2. **Order Splitting Logic**  
* Detect orders requiring multiple fulfillment locations  
* Split into sub-orders with distinct pickup points  
* Maintain parent-child order relationship for tracking  
3. **ETA Calculation Engine**  
* Compute estimated delivery time based on fulfillment location and delivery type  
* Factor in pickup preparation time per location  
* Update ETA dynamically as order progresses  
4. **Status Update System**  
* Push order status changes to Magento (fulfillment location assigned, ready for pickup, dispatched)  
* Maintain internal status log for audit trail

## **3.4 Route Optimization**

**Functional Requirements**

1. **Multi-Stop Routing Algorithm**  
* Optimize driver routes for multiple deliveries  
* Minimize total travel time while respecting delivery windows  
* Support for pickup consolidation (multiple pickups before delivery run)  
2. **Zone Clustering Logic**  
* Group deliveries by geographic zone  
* Assign clustered orders to drivers for route efficiency  
* Configurable zone boundaries  
3. **Driver Assignment System**  
* Match optimized routes to available drivers  
* Consider driver current location and capacity  
* Output assignment decisions to Delivery Admin Platform  
4. **Real-time Tracking Integration**  
* Receive driver location updates  
* Recalculate ETAs based on actual progress  
5. **Auto-Adjust Logic**  
* Detect route deviations and delays  
* Trigger re-routing when conditions change significantly

## **3.5 Human-in-the-Loop Review**

**Functional Requirements**

1. **Decision Oversight Interface**  
* Dashboard displaying AI routing decisions pending review  
* Show scoring breakdown per decision for transparency  
* One-click approval or manual override capability  
2. **Exception Handling Workflow**  
* Queue for orders flagged by algorithm (no viable location, inventory discrepancy, edge cases)  
* Manual resolution workflow with audit logging  
3. **Quality Assurance Dashboard**  
* Display algorithm accuracy metrics  
* Track override frequency and reasons  
* Feedback loop for algorithm improvement  
4. **Override Controls System**  
* Manual override capability for any automated decision  
* Override reason capture for analytics  
* Role-based override permissions

## **3.6 Configuration**

**Functional Requirements**

1. **Store Enable/Disable System**  
* Toggle fulfillment locations on/off without code deployment  
* Immediate effect on routing algorithm  
2. **Backend Configuration Panel**  
* Adjust scoring weights without code changes  
* Configure delivery time thresholds per delivery type  
* Set capacity limits per fulfillment location  
3. **Auto-Failover Logic**  
* Automatic fallback when integration dependencies fail  
* Graceful degradation to manual routing mode  
4. **Cache Management System**  
* Cache inventory data with configurable TTL  
* Cache distance calculations for common routes  
* Manual cache invalidation capability

## **3.7 System Outputs**

**Functional Requirements**

1. **Magento Integration**  
* Push fulfillment location assignment to order  
* Update order status through fulfillment lifecycle  
2. **Delivery Admin Platform API**  
* Push routed tasks with pickup location, delivery address, optimized route  
* Include driver assignment recommendations  
3. **SMS Gateway Integration**  
* Staff notifications for new order assignments  
* Driver alerts for route changes  
4. **WhatsApp Integration**  
* Customer notifications: order confirmed, driver dispatched, ETA updates  
5. **Analytics Dashboard**  
* Real-time operational metrics  
* Performance reports and trend analysis

## **3.8 Fulfillment Locations (Initial)**

Phase 1 deployment covers two locations:

| Code | Location | Type | Role |
| :<hr class="my-8 border-t border-gray-300">- | :<hr class="my-8 border-t border-gray-300">- | :<hr class="my-8 border-t border-gray-300">- | :<hr class="my-8 border-t border-gray-300">- |
| 999 | Warehouse | Central FC | Primary fulfillment, full inventory |
| 101 | Al Rai | MFC | Quick commerce, high-velocity SKUs |

# **4\. Phase 2 Scope**

Phase 2 introduces predictive analytics and inventory optimization. Runs in parallel with Phase 1 from Day 0, with full capability expected by Month 3\. Requires high-quality historical data (post-COVID trends) for model training.

## **4.1 Model Training**

1. **Historical Data Ingestion Pipeline**  
* Ingest historical sales data from Dynamics AX 2012  
* Process POS transaction history across all locations  
* Clean and normalize data for model consumption  
2. **Pattern Recognition Development**  
* Identify sales patterns by SKU, location, time period  
* Detect seasonal trends and promotional impacts  
3. **Continuous Learning Framework**  
* Model retraining pipeline with new transaction data  
* Performance monitoring and drift detection

## **4.2 Range Analysis**

1. **Online Sales Data Integration**  
* E-commerce transaction analysis by SKU and category  
2. **Walk-in Sales Data Integration**  
* POS transaction analysis across retail locations  
3. **Sell-Through Rate Calculation**  
* SKU-level sell-through metrics per location  
* Category performance comparison  
4. **Demand Pattern Analysis**  
* Day-of-week and time-of-day demand curves  
* Geographic demand distribution

## **4.3 AI Optimization**

1. **Seasonality Analysis Module**  
* Annual seasonality patterns (holidays, back-to-school, Ramadan)  
* Promotional period impact modeling  
2. **SKU-Level Forecast Engine**  
* Demand forecasting at individual SKU level  
* Location-specific demand predictions  
* Confidence intervals for forecast accuracy  
3. **Stock Recommendations System**  
* Optimal stock level recommendations per SKU per location  
* Replenishment timing suggestions  
4. **Rebalancing Alerts System**  
* Proactive alerts when inventory imbalance detected  
* Inter-location transfer recommendations

## **4.4 Phase 2 Outputs**

1. **Inventory Reports**  
* Rebalancing alerts with actionable recommendations  
* Stock level recommendations with forecast context

# **5\. Out of Scope**

The following are explicitly excluded from both Phase 1 and Phase 2:

* Driver management and task assignment UI (handled by Delivery Admin Platform)  
* Driver mobile application (separate system)  
* Customer-facing order tracking interface  
* Payment processing and COD management  
* Order creation and editing (orders received from source systems)  
* Proof of delivery capture (handled by Driver App)  
* Direct AX 2012 API development (FWT in-house responsibility)  
* Direct Magento webhook development (FWT in-house responsibility)  
* Procurement and purchase order management

# **6\. Technical Constraints & Assumptions**

## **6.1 Assumptions**

1. FWT in-house team will develop Dynamics AX 2012 APIs per specifications provided; contract to be finalized during technical design.  
2. FWT in-house team will implement Magento webhook endpoints per specifications provided.  
3. Historical sales data (minimum 2 years post-COVID) is available and accessible for model training.  
4. Delivery Admin Platform development proceeds in parallel; API contracts to be coordinated.  
5. Geofence boundaries for stores and delivery zones will be provided by operations team.  
6. Google Maps API quotas and billing approved by FWT.

## **6.2 Technical Constraints**

| Constraint | Details |
| :<hr class="my-8 border-t border-gray-300">- | :<hr class="my-8 border-t border-gray-300">- |
| Orchestration Platform | n8n on Azure; custom code for deterministic tasks |
| ERP Integration | Dynamics AX 2012; no existing APIs (to be built) |
| Map Provider | Google Maps API (Distance Matrix, Directions) |
| Initial Locations | 2 locations (Phase 1); scalable to 6 (Testing/Optimization) |
| Order Volume | Support 150 daily orders (MVP); scalable to 300+ |
| Delivery Types | Normal (\<3h), Express (\~2h), Super Express (\<1h) |

## **6.3 Non-Functional Requirements**

| Requirement | Target |
| :<hr class="my-8 border-t border-gray-300">- | :<hr class="my-8 border-t border-gray-300">- |
| Availability | 99.5% uptime during operational hours (7 AM \- 11 PM Kuwait) |
| Routing Decision Latency | \< 5 seconds from order receipt to location assignment |
| Routing Accuracy | \> 95% optimal location selection (validated against manual review) |
| Data Retention | 12 months decision history; model training data retained indefinitely |

# **7\. Acceptance Criteria**

## **7.1 Phase 1 Complete When:**

* Orders received from Magento webhooks and processed within 5 seconds  
* Scoring algorithm correctly ranks fulfillment locations based on inventory, distance, capacity, priority  
* Order splitting logic correctly handles multi-location fulfillment scenarios  
* Route optimization produces efficient multi-stop routes  
* Human-in-the-loop interface displays pending decisions with scoring breakdown  
* Override controls function correctly with audit logging  
* Routed tasks successfully pushed to Delivery Admin Platform  
* Customer notifications delivered via WhatsApp  
* Warehouse (999) and Al Rai (101) operational with inventory sync  
* System handles 150 daily orders without degradation

## **7.2 Phase 2 Complete When:**

* Historical data pipeline ingests and processes sales data  
* Demand forecasting produces SKU-level predictions with measurable accuracy  
* Stock recommendations generated and delivered to operations team  
* Rebalancing alerts trigger proactively before stockouts  
* Continuous learning pipeline retrains models with new data

*— End of Document —*