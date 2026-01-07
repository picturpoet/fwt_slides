# **Driver Mobile Application**

Product Requirements Document

Version 1.0 | December 2025

# **1\. Executive Summary**

This document defines requirements for the Driver Mobile Application, a Flutter-based app (Android and iOS) that enables delivery drivers to receive assigned routes, execute pickups and deliveries, capture proof of delivery, and communicate with warehouse operations. The app operates as the execution layer for routes scheduled by the Trip Scheduler and managed via the Admin & Analytics Platform.

## **Business Context**

The application supports a toy retail delivery operation in Kuwait with one warehouse and six stores. Drivers execute 100-150 daily deliveries, with 10 drivers typically online concurrently from a pool of 30\. Routes may include multi-point pickups (warehouse and/or stores) before customer delivery. The app replaces an existing basic Android APK with a cross-platform Flutter solution.

# **2\. System Context**

## **System Architecture Overview**

| System | Role & Integration |
| :---- | :---- |
| **Trip Scheduler** | Creates optimized routes from AX 2012 orders. Pushes scheduled routes to Admin Platform. Defines micro-task sequence within each route. |
| **Admin Platform** | Receives routes from Trip Scheduler. Assigns routes to drivers. Can manually reorder micro-tasks. Sends route assignments to Driver App. Receives status updates and POD from Driver App. |
| **Driver App** (this PRD) | Receives assigned routes. Guides driver through micro-tasks. Captures POD. Reports location and status. Provides chat with warehouse/admin. |
| **External Apps** | Google Maps (navigation), Phone (customer calls), Camera (POD capture). Driver App launches these via deep links; does not embed functionality. |

**Data Flow:** Trip Scheduler → Admin Platform → Driver App → Admin Platform (status/POD)

## **Route & Micro-Task Model**

Each route corresponds to one customer order and contains multiple micro-tasks executed sequentially.

**Micro-Task Types**

| Type | Description |
| :---- | :---- |
| Pickup | Collect items from warehouse or store location |
| Dropoff | Deliver items to customer location |
| State Update | Terminal status: Delivered, Rejected by Customer, Customer Unavailable, Wrong Address, Partial Delivery |

**Micro-Task States**

* **Assigned:** Micro-task received by driver, awaiting action  
* **Started:** Driver has begun execution (en route or at location)  
* **Completed:** Micro-task finished (items collected, delivered, or terminal state recorded)

# **3\. MVP Scope**

MVP delivers core driver workflow: authentication, route execution, POD capture, and warehouse communication. Development target: 10 weeks, coordinated with Admin Platform timeline.

## **3.1 Authentication & Onboarding**

**Functional Requirements**

1. **Splash Screen**  
   * Animated launch screen (16:9 aspect ratio)  
   * Brand assets displayed during app initialization  
2. **Login**  
   * Credential-based authentication (phone/email \+ password)  
   * Session persistence with secure token storage  
   * Localized UI assets (Arabic/English)  
3. **First-Login Training**  
   * Mandatory training flow before driver can go Online  
   * Module-based progression: each module contains video/image \+ description \+ required action to proceed  
   * Training completion flag stored; subsequent logins bypass training

## **3.2 Home Dashboard**

**Functional Requirements**

4. **Driver Status Toggle**  
   * Online/Offline toggle prominently displayed  
   * Online: Driver available for route assignments; location tracking active  
   * Offline: Driver unavailable; location tracking paused  
   * Status synced to Admin Platform in real-time  
5. **Performance Stats Widget**  
   * Rolling 7-day metrics displayed by default  
   * Deliveries Made: Count of completed dropoff micro-tasks  
   * Hours Online: Cumulative time in Online status  
   * Distance Covered: Total km traveled (received from backend)  
6. **Current Route Widget**  
   * Interactive card showing active route assignment  
   * Mini-map preview with pickup/dropoff markers  
   * Next micro-task summary (location name, type)  
   * Tap to expand to full Route Detail view  
7. **Navigation Actions**  
   * Routes (History): Access completed route list  
   * Chat: Access persistent warehouse communication thread  
   * Help Center: Access training modules and support

## **3.3 Route Execution**

**Functional Requirements**

8. **Route Detail View**  
   * Full route overview with all micro-tasks listed in sequence  
   * Visual status indicators per micro-task (Assigned/Started/Completed)  
   * Customer order reference visible  
   * Estimated total route duration/distance  
9. **Micro-Task Execution Flow**  
   * Start button transitions micro-task from Assigned → Started  
   * Navigate button launches Google Maps with destination coordinates  
   * Arrive/Complete button marks micro-task as Completed (triggers POD for dropoffs)  
   * Sequential enforcement: next micro-task unlocks only after current completes  
10. **Pickup Micro-Task**  
    * Location details: warehouse/store name, address  
    * Items to collect (if available from backend)  
    * Confirm Pickup action to complete  
11. **Dropoff Micro-Task**  
    * Customer name, address, contact phone  
    * Call Customer button: launches phone app with customer number  
    * Delivery window (if specified)  
    * Complete Delivery action triggers POD capture  
12. **Terminal State Selection**  
    * Driver selects outcome after dropoff attempt:  
    * Delivered (success)  
    * Rejected by Customer  
    * Customer Unavailable  
    * Wrong Address  
    * Partial Delivery (with item selection if applicable)

## **3.4 Proof of Delivery**

**Functional Requirements**

13. **Photo Capture**  
    * Launches device camera app for photo capture  
    * Photo required before dropoff can be marked complete  
    * Preview and retake option before confirmation  
14. **EXIF Data Preservation**  
    * Timestamp and GPS coordinates extracted from photo metadata  
    * EXIF data validated and stored with task record  
    * Fallback: if EXIF unavailable, capture device location at photo time  
15. **Offline POD Handling**  
    * Photos stored locally if network unavailable  
    * Automatic upload retry when connectivity restored  
    * Visual indicator for pending uploads

## **3.5 Communication**

**Functional Requirements**

16. **Warehouse/Admin Chat**  
    * Single persistent chat thread per driver  
    * Available at all times (not route-specific)  
    * Text messages only (MVP)  
    * Message history retained and scrollable  
    * Push notification for new incoming messages  
17. **Customer Call**  
    * Call button visible on dropoff micro-task detail  
    * Launches phone app with customer number pre-filled

## **3.6 Routes History**

**Functional Requirements**

18. **Completed Routes List**  
    * Chronological list of completed routes  
    * Summary per route: date, customer order ID, stop count, terminal state  
    * Tap to view route detail with all micro-tasks  
19. **Route Detail (Historical)**  
    * Read-only view of micro-task sequence  
    * Timestamps per state transition  
    * POD photo viewable (if captured)

## **3.7 Training & Help**

**Functional Requirements**

20. **Training Modules**  
    * Module structure: video or image \+ description \+ required action  
    * Progressive unlock: complete current module to access next  
    * Content loaded from backend (CMS-ready structure)  
21. **Help Center Access**  
    * Re-watch any training module at any time  
    * Accessible from dashboard navigation

## **3.8 Location & Background Services**

**Functional Requirements**

22. **Location Tracking**  
    * Active when driver status is Online  
    * Location updates sent to Admin Platform at configurable interval  
    * Background location permission required  
23. **Offline Resilience**  
    * State changes queued locally when offline  
    * Automatic sync when connectivity restored  
    * Visual indicator when operating offline  
24. **Push Notifications**  
    * New route assignment  
    * Route modification (micro-task reordering)  
    * New chat message from admin/warehouse  
    * Implementation: FCM (Android) / APNs (iOS) — final choice at development time

# **4\. Phase II Scope**

Phase II extends driver capabilities with enhanced communication, additional POD methods, and richer analytics. Target: 6-8 weeks post-MVP launch.

## **4.1 Enhanced Communication**

1. **Route-Specific Chat Threads**  
   * Separate chat thread per route/order  
   * Context preserved for issue resolution  
2. **Image/File Sharing in Chat**  
   * Send photos to warehouse (e.g., damaged items, blocked access)  
   * Receive documents from admin  
3. **WhatsApp Customer Integration**  
   * Launch WhatsApp with customer number for text communication

## **4.2 Extended POD Methods**

4. **Signature Capture**  
   * On-screen signature pad  
   * Signature stored as image with timestamp  
5. **OTP Verification**  
   * Customer provides OTP sent via SMS  
   * Driver enters OTP to confirm delivery  
6. **Barcode/QR Scanning**  
   * Scan package barcode to confirm correct item delivered

## **4.3 Cash on Delivery**

7. **COD Collection**  
   * Display amount due on dropoff screen  
   * Confirm cash collected as part of completion flow  
8. **Driver Wallet View**  
   * Running balance of collected cash  
   * Settlement history

## **4.4 Enhanced Analytics**

9. **Extended Stats Period Selection**  
   * Today, This Week, This Month, Custom Range  
10. **Performance Trends**  
    * Visual charts for delivery volume over time  
    * On-time delivery percentage

## **4.5 Earnings & Incentives**

11. **Earnings Dashboard**  
    * View earnings per route/day/week  
    * Incentive progress tracking  
    * Note: Display only; payroll remains out of scope

# **5\. Out of Scope**

The following are explicitly excluded from both MVP and Phase II:

* In-app turn-by-turn navigation (external Google Maps used)  
* Route optimization or resequencing by driver  
* Task rejection by driver (all assigned tasks must be attempted)  
* Driver payroll, payout, or compensation calculation  
* Vehicle maintenance tracking  
* Fuel tracking or reimbursement  
* Multi-language beyond Arabic/English  
* Direct integration with AX 2012 or Trip Scheduler (Admin Platform intermediates)

# **6\. Technical Constraints & Assumptions**

## **6.1 Assumptions**

1. Admin Platform API contracts finalized before driver app development begins.  
2. All drivers have smartphones meeting minimum OS requirements with reliable GPS.  
3. Google Maps installed on all driver devices.  
4. Network connectivity across Kuwait delivery zones supports periodic location updates and photo uploads.  
5. Training content (videos/images) provided by operations team before launch.

## **6.2 Technical Constraints**

| Constraint | Details |
| :---- | :---- |
| Framework | Flutter (Dart) — single codebase for Android and iOS |
| Database | PostgreSQL |
| Android Support | Android 14 and 15 (API level 34-35) |
| iOS Support | iOS 17 and 18 |
| Navigation | External Google Maps launch via deep link |
| Camera | External camera app launch; EXIF extraction on return |
| Phone Calls | External phone app launch via tel: URI |
| Communication APIs | WhatsApp API, Octopus API |
| Localization | Arabic (RTL) and English supported |

## **6.3 Non-Functional Requirements**

| Requirement | Target |
| :---- | :---- |
| App Launch Time | \< 3 seconds to interactive dashboard (warm start) |
| Location Update Frequency | Every 10-30 seconds when Online (configurable server-side) |
| Battery Impact | \< 15% battery drain per 8-hour shift with continuous location tracking |
| Offline Queue Capacity | Store up to 50 state changes and 10 POD photos locally |
| POD Upload | \< 10 seconds per photo on 4G connection |

# **7\. MVP Acceptance Criteria**

MVP is complete when:

* Driver can authenticate and complete mandatory training on first login  
* Online/Offline toggle correctly starts and stops location tracking  
* Assigned routes appear on dashboard and driver can view full micro-task sequence  
* Driver can execute micro-tasks sequentially: Start → Navigate (external maps) → Complete  
* POD photo capture with EXIF data successfully uploads and links to task  
* Terminal states (Delivered, Rejected, Unavailable, Wrong Address, Partial) can be recorded  
* Persistent chat thread with warehouse/admin sends and receives text messages  
* Call Customer launches phone app with correct number  
* Routes history displays completed routes with timestamps and POD photos  
* Offline state changes and POD photos queue and sync when connectivity restored  
* App functions on Android 14/15 and iOS 17/18 without crashes

*— End of Document —*