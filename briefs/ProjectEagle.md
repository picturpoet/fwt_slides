# **Delivery Admin & Analytics Platform**

Product Requirements Document

Version 1.0 | December 2025

# **1\. Executive Summary**

This platform provides centralized task management, real-time tracking, and operational analytics for delivery operations across one warehouse and six retail stores in Kuwait. The system receives scheduled delivery tasks from an upstream Trip Scheduler (which pulls from AX 2012 ERP) and enables dispatchers to monitor, assign, and analyze delivery performance. Drivers execute tasks via a companion Flutter mobile application.

## **Business Context**

The platform supports a toy retail operation handling 100-150 daily orders with 10 concurrent drivers (30 total driver pool). Order types include immediate in-store purchases and scheduled deliveries for large items (e.g., home gyms) that require logistics coordination regardless of purchase location. Orders originate from POS, e-commerce (Magento), and a customer mobile app.

# **2\. System Context**

## **System Architecture Overview**

| System | Role & Integration |
| :---- | :---- |
| **AX 2012 (ERP)** | Order management and master data. No direct integration with this platform. |
| **Trip Scheduler** | Upstream system. Pulls orders from AX 2012, schedules trips, and pushes ready-to-execute tasks via API to this platform. |
| **Admin Platform** (this PRD) | Receives scheduled tasks, enables assignment/monitoring, provides analytics. Web-based dashboard for dispatchers and managers. |
| **Driver App** | Flutter-based (Android/iOS). Receives task assignments, provides navigation, captures POD via photo with EXIF data. |
| **Magento** | E-commerce and POS order source. Orders flow to AX 2012, not directly to this platform. |

**Data Flow:** Magento/POS → AX 2012 → Trip Scheduler → Admin Platform → Driver App

## **2.2 Frontend Architecture**

The Admin Platform will be a sidebar-navigation based web app. Reference designs/screens will be provided based on Stitch by Google.

**Sidebar Navigation Structure**

*   **Top Section**
    1.  **Dashboard**
    2.  **Eagle View** (Live Map with fleet and stores)
    3.  **Orders**
    4.  **Analytics**
*   **Bottom Section**
    5.  **Audit Log**
    6.  **Settings**
    7.  **Support**

**Additional Views**

*   **Auth/Login View**: Standard authentication interface.

## **2.3 Key Integrations**

*   **Google Maps**: Serves as the foundation for the **Eagle View**, providing real-time fleet and store tracking.
*   **Power BI**: Embedded within the **Analytics** view to provide advanced operational reporting.

# **3\. MVP Scope**

MVP delivers core operational capability: receive tasks, assign to drivers, track execution, verify delivery, and report on performance. Target: operational readiness within 12 weeks of development start.

## **3.1 Task Management**

**Functional Requirements**

1. **Task Panel with State Management**  
   * Three states: Unassigned (awaiting driver), Assigned (allocated, not started), Completed (delivered)  
   * Real-time state transitions visible across all logged-in dispatchers  
   * Filterable/sortable by state, driver, date, location  
2. **Task Ingestion via API**  
   * Endpoint to receive tasks from Trip Scheduler/Intelligence Engine  
   * Task payload: order ID, pickup location(s), delivery location, customer details, time window, item description  
   * Support for multi-point pickups (warehouse \+ stores) within single task  
3. **Manual Task Creation**  
   * UI form for ad-hoc task creation (edge cases, corrections)  
   * Required fields: pickup location, delivery location, customer contact, delivery window  
4. **Task Details**  
   * Description, delivery time window, geofence reference  
   * Support for attached images (product photos)

## **3.2 Real-Time Tracking & Monitoring**

**Functional Requirements**

5. **Live Map View**  
   * Google Maps integration (primary) with option to switch to open-source alternative (e.g., OpenStreetMap/Leaflet)  
   * Display all active drivers with real-time position updates  
   * Show task pickup and delivery markers  
6. **Driver Status Panel**  
   * Three states: Free (available), Busy (on task), Inactive (off-duty)  
   * Status auto-updates based on task assignment and completion  
   * Manual override for dispatcher corrections  
7. **Live Tracking Links**  
   * Generate shareable URLs for customer/store visibility into driver location  
   * Links auto-expire after task completion  
8. **Push Notifications**  
   * Task status updates to relevant stakeholders (driver assigned, en route, delivered)

## **3.3 Assignment System**

**Functional Requirements**

9. **Manual Assignment**  
   * Dispatcher selects driver from available pool  
   * Assignment confirmation required from driver app  
10. **Auto-Allocation: Nearest Available**  
    * System identifies closest free driver based on GPS  
    * Fallback to manual if no driver accepts within configurable timeout  
11. **Auto-Allocation: Round Robin**  
    * Equal workload distribution across driver pool  
    * Configurable weighting factors (optional)  
12. **Geofencing**  
    * Define operational boundaries for each store/zone  
    * Restrict auto-assignment to drivers within relevant geofence

## **3.4 Driver Management**

**Functional Requirements**

13. **Driver Onboarding**  
    * Individual driver registration via admin UI  
    * Bulk import via CSV (support up to 100 drivers per upload)  
14. **Driver Profile**  
    * Name, phone, credentials, team assignment, vehicle details (license plate)  
    * Driver type label: Payroll vs. Third-Party (visible in UI)  
15. **Team Structure**  
    * Organize drivers by operational zone (warehouse, store clusters)

## **3.5 Proof of Delivery**

**Functional Requirements**

16. **Photo-Based POD**  
    * Driver captures delivery photo via app  
    * EXIF data (timestamp, GPS coordinates) preserved and validated  
    * Photo displayed in admin dashboard upon completion  
17. **POD Storage & Retrieval**  
    * Photos linked to task record  
    * Searchable by order ID, date, driver

## **3.6 Communication**

**Functional Requirements**

18. **Admin-Driver Chat**  
    * In-platform messaging between dispatcher and driver  
    * Message history retained per task  
19. **Click-to-Call**  
    * Direct dial to customer/warehouse from task detail screen

## **3.7 Analytics & Reporting**

**Functional Requirements**

20. **Performance Metrics Dashboard**  
    * Task completion rate (daily, weekly, monthly)  
    * Average delivery time (order-to-delivery)  
    * Driver utilization (busy vs. idle time)  
    * Tasks per driver per day  
21. **Operational Reports**  
    * Completed tasks by date range  
    * Tasks by zone/store  
    * Export to CSV  
22. **Driver Performance**  
    * Distance covered  
    * Time per task  
    * On-time delivery rate

## **3.8 Access Control**

**Functional Requirements**

23. **Role-Based Permissions**  
    * Admin: Full access (driver management, all tasks, all analytics, system configuration)  
    * Dispatcher: Task management, driver monitoring, limited analytics

# **4\. Phase II Scope**

Phase II extends operational capability with advanced automation, third-party logistics integration, financial tracking, and predictive analytics. Target: 8-12 weeks post-MVP launch.

## **4.1 Advanced Assignment Modes**

1. **Batch Wise Allocation**  
   * Tasks within defined radius offered to available drivers  
2. **Send to All (Broadcast)**  
   * Broadcast task to all available drivers; first acceptance wins  
3. **One by One (Sequential)**  
   * Offer to drivers sequentially with configurable timeout and rejection fallback  
4. **FIFO Processing**  
   * Strict sequential task processing based on creation time

## **4.2 Third-Party Logistics (Merchant) Support**

5. **Merchant Onboarding**  
   * Register 3PL providers with company details  
   * Merchant-specific driver pools  
6. **Merchant Access Control**  
   * Restricted visibility: Merchants see only their assigned tasks and drivers  
   * Merchant-specific analytics subset  
7. **Driver Labeling**  
   * Clear visual distinction between payroll drivers and 3PL drivers

## **4.3 Extended Task Creation**

8. **Bulk CSV Import**  
   * Upload multiple tasks via standardized CSV template  
   * Validation and error reporting pre-import  
9. **Custom Task Templates**  
   * Industry-specific fields (items, quantity, amount, special instructions)

## **4.4 Cash on Delivery Management**

10. **COD Tracking**  
    * Track cash collected per task  
    * Daily cash reconciliation reports  
11. **Driver Wallet**  
    * Virtual balance tracking for collected cash  
    * Settlement workflow

## **4.5 Extended Communication**

12. **Driver-Customer Chat**  
    * In-app messaging during active task only  
13. **Driver-Store Chat**  
    * Communication channel during pickup  
14. **WhatsApp Integration**  
    * Optional external channel for driver-customer communication

## **4.6 Advanced Analytics**

15. **Extended Metrics**  
    * Task acceptance/rejection ratios  
    * Driver competence ratings (manual or derived)  
16. **AI-Powered Insights (Beta)**  
    * Delivery time prediction  
    * Bottleneck identification  
    * Optimization recommendations

## **4.7 Extended POD Methods**

17. **Signature Capture**  
18. **OTP Verification**  
19. **Barcode Scanning**  
20. **PDF Export**  
    * Complete delivery reports with timestamps, images, barcodes

## **4.8 Integrations & Extensions**

21. **Payment Gateway Integration**  
22. **E-commerce Platform Connectors**  
    * Shopify, WooCommerce (if expanding beyond Magento)  
23. **Open API**  
    * External system integration endpoints  
24. **Data Export API**  
    * Push task data, POD, and delivery confirmations to external systems

## **4.9 Document Management**

25. **Driver Document Upload**  
    * License, certifications, ID verification storage

# **5\. Out of Scope**

The following are explicitly excluded from both MVP and Phase II:

* Driver payroll and compensation management  
* Order management (handled by AX 2012\)  
* Trip scheduling and route optimization (handled by Trip Scheduler)  
* Direct integration with AX 2012 or Magento  
* Multi-tenant capability (single-organization deployment)  
* Customer-facing application features  
* Inventory management  
* Vehicle maintenance and fleet management

# **6\. Technical Constraints & Assumptions**

## **6.1 Assumptions**

1. Trip Scheduler will expose a well-documented API for pushing tasks; contract to be finalized during technical design.  
2. Driver app (Flutter) development proceeds in parallel with this platform; API contracts to be coordinated.  
3. All drivers have smartphones capable of running the Flutter app with reliable GPS.  
4. Network connectivity across Kuwait delivery zones is sufficient for real-time updates.  
5. Geofence boundaries for stores and zones will be provided by operations team.

## **6.2 Technical Constraints**

| Constraint | Details |
| :---- | :---- |
| Map Provider | Google Maps primary; OpenStreetMap/Leaflet as cost-optimized fallback |
| Driver Volume | Support up to 50 concurrent drivers (MVP), scalable to 100+ (Phase II) |
| Task Volume | Support up to 300 daily tasks (MVP), scalable to 500+ (Phase II) |
| POD Method | Photo with EXIF validation (MVP); extended methods in Phase II |
| Browser Support | Chrome, Safari, Edge (latest two versions) |

## **6.3 Non-Functional Requirements**

| Requirement | Target |
| :---- | :---- |
| Availability | 99.5% uptime during operational hours (7 AM \- 11 PM Kuwait time) |
| Location Update Latency | \< 10 seconds from driver app to admin dashboard |
| Dashboard Load Time | \< 3 seconds initial load |
| Data Retention | 12 months task history; POD images retained per compliance requirements |

# **7\. MVP Acceptance Criteria**

MVP is complete when:

* Tasks can be received from Trip Scheduler API and displayed in admin dashboard  
* Dispatchers can manually assign tasks to drivers and see confirmation  
* Nearest Available and Round Robin auto-allocation modes function correctly  
* Live map displays driver locations with \< 10 second latency  
* Photo-based POD with EXIF validation completes tasks successfully  
* Admin-driver chat functions during active tasks  
* Core analytics dashboard displays completion rates and driver utilization  
* Role-based access control restricts dispatcher permissions appropriately  
* System handles 150 daily tasks with 10 concurrent drivers without degradation

*— End of Document —*