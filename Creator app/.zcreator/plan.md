This app will manage ad-hoc college transport requests from submission through approval, vehicle/driver assignment, driver notification, and trip completion. It includes master records for staff, departments, transport team members, vehicles, and drivers, plus dashboards, reports, permissions, and mobile-friendly navigation.

## User Profiles

Create the login access categories used throughout the app. These shell profiles establish who can request trips, supervise activity, manage transport, and complete assigned trips.

Create custom shell profile files under Permissions/Profiles/ only. Profiles to create:
1. Staff — custom profile, Predefined:false. Intended access: create transport requests, view their own request progress, see assigned vehicle/driver details after assignment, no master-data management.
2. Department_Manager — custom profile, Predefined:false. Intended access: read-only oversight of requests and reports for college management; no approval/assignment authority in this app.
3. Transport_Manager — custom profile, Predefined:false. Intended access: manage master data, approve/reject requests, assign vehicle and driver, complete trips, and access all operational reports/dashboard.
4. Driver — custom profile, Predefined:false. Intended access: view assigned trips, acknowledge/complete assigned trips, and read only the limited trip details needed to execute the journey.

Only write name/type shell declarations. The final Permissions segment will edit these files to add complete ModulePermissions after all forms/reports/pages exist. No roles or sharing hierarchy in this segment.

**Implementation notes:** Write only shell profile declarations for custom profiles; do not add ModulePermissions yet. Do not write default Administrator/Developer profiles.

## Departments

Maintain college departments so requests and staff can be categorized cleanly. This supports filtering and management reporting by department.

Create one form: Departments.

Form: Departments
- Display name: Departments.
- Fields:
  - Section: Department_Information, type=section, first field, row 1 column 0.
  - Department_Name, type=text, must have, unique, display name Department Name.
  - Department_Code, type=text, unique, display name Department Code.
  - Manager_Name, type=text, display name Manager Name.
  - Manager_Email, type=email, display name Manager Email.
  - Status, type=picklist, must have, values: Active, Inactive; default/initial Active.
  - Notes, type=textarea.
- Actions: standard Submit/Reset on add and Update/Cancel on edit.

Reports:
1. All_Departments — default list report from Departments. Columns: Department_Name, Department_Code, Manager_Name, Manager_Email, Status. Filters: Status, Department_Name. Sort Department_Name ascending. Profiles intended: Transport_Manager full, Department_Manager read-only.
2. Active_Departments — list report from Departments where Status == Active. Columns: Department_Name, Department_Code, Manager_Name, Manager_Email. Filters: Department_Name. Sort Department_Name ascending. Profiles intended: Staff read-only, Transport_Manager full, Department_Manager read-only.

Workflows: none beyond declarative validation/defaults.

**Implementation notes:** Define Departments before Staff_Directory because Staff_Directory looks up Departments. Use declarative mandatory/unique properties for required department name/code where applicable.

## Staff_Directory

Maintain staff identities and department association so requests can be prefilled and tracked by requester. This avoids free-text staff details and supports email notifications.

Create one form: Staff_Directory.

Form: Staff_Directory
- Display name: Staff Directory.
- Fields:
  - Section: Staff_Information, type=section, first field, row 1 column 0.
  - Staff_ID, type=text, unique, display name Staff ID.
  - Staff_Name, type=text, must have, display name Staff Name.
  - Email, type=email, must have, unique, display name Email.
  - Phone, type=phonenumber, display name Phone.
  - Department, type=picklist lookup to Departments.ID, must have, displayformat Department_Name, display name Department.
  - Staff_Role, type=picklist, values: Teaching, Non-Teaching, Administration, Management, Other; display name Staff Role.
  - Active_Status, type=picklist, must have, values: Active, Inactive; default/initial Active.
  - Notes, type=textarea.
- Actions: standard Submit/Reset on add and Update/Cancel on edit.

Reports:
1. All_Staff — default list report from Staff_Directory. Columns: Staff_ID, Staff_Name, Email, Phone, Department, Staff_Role, Active_Status. Filters: Department, Staff_Role, Active_Status. Sort Staff_Name ascending. Profiles intended: Transport_Manager full, Department_Manager read-only.
2. Active_Staff_By_Department — list report from Staff_Directory where Active_Status == Active. Columns: Staff_Name, Email, Phone, Department, Staff_Role. Filters: Department, Staff_Role. Group by Department ascending. Sort Staff_Name ascending. Profiles intended: Staff read-only, Department_Manager read-only, Transport_Manager full.

Workflows: none beyond declarative validation/defaults.

**Implementation notes:** Depends on Departments. Use lookup to Departments with a human-readable display field. Staff emails must be unique for login matching via zoho.loginuserid.

## Transport_Team

Maintain the transport office team and approval recipients. This list is used to notify active transport managers when new requests arrive.

Create one form: Transport_Team.

Form: Transport_Team
- Display name: Transport Team.
- Fields:
  - Section: Team_Member_Information, type=section, first field, row 1 column 0.
  - Member_Name, type=text, must have, display name Member Name.
  - Email, type=email, must have, unique, display name Email.
  - Phone, type=phonenumber, display name Phone.
  - Team_Role, type=picklist, must have, values: Transport Manager, Coordinator, Dispatcher; display name Team Role.
  - Can_Approve, type=checkbox, initial/default true, display name Can Approve Requests.
  - Active_Status, type=picklist, must have, values: Active, Inactive; default/initial Active.
  - Notes, type=textarea.
- Actions: standard Submit/Reset on add and Update/Cancel on edit.

Reports:
1. All_Transport_Team — default list report from Transport_Team. Columns: Member_Name, Email, Phone, Team_Role, Can_Approve, Active_Status. Filters: Team_Role, Can_Approve, Active_Status. Sort Member_Name ascending. Profiles intended: Transport_Manager full.
2. Active_Approvers — list report from Transport_Team where Active_Status == Active && Can_Approve == true. Columns: Member_Name, Email, Phone, Team_Role. Filters: Team_Role. Sort Member_Name ascending. Profiles intended: Transport_Manager full.

Workflows: none beyond declarative validation/defaults.

**Implementation notes:** Transport_Requests workflows will look up active approvers from this form by role and active status.

## Drivers

Maintain driver records, contact information, licence details, and current availability. These records are used during trip assignment and driver notification.

Create one form: Drivers.

Form: Drivers
- Display name: Drivers.
- Fields:
  - Section: Driver_Information, type=section, first field, row 1 column 0.
  - Driver_Name, type=text, must have, display name Driver Name.
  - Driver_Email, type=email, must have, unique, display name Driver Email.
  - Driver_Phone, type=phonenumber, display name Driver Phone.
  - License_Number, type=text, must have, unique, display name License Number.
  - License_Expiry, type=date, display name License Expiry.
  - Badge_Number, type=text, display name Badge Number.
  - Active_Status, type=picklist, must have, values: Active, Inactive; default/initial Active.
  - Availability_Status, type=picklist, must have, values: Available, Assigned, On Leave, Inactive; default/initial Available.
  - Notes, type=textarea.
- Actions: standard Submit/Reset on add and Update/Cancel on edit.

Reports:
1. All_Drivers — default list report from Drivers. Columns: Driver_Name, Driver_Email, Driver_Phone, License_Number, License_Expiry, Badge_Number, Active_Status, Availability_Status. Filters: Active_Status, Availability_Status. Sort Driver_Name ascending. Profiles intended: Transport_Manager full.
2. Available_Drivers — list report from Drivers where Active_Status == Active && Availability_Status == Available. Columns: Driver_Name, Driver_Email, Driver_Phone, License_Expiry, Availability_Status. Filters: Availability_Status. Sort Driver_Name ascending. Profiles intended: Transport_Manager full.
3. Driver_License_Expiry — list report from Drivers where Active_Status == Active. Columns: Driver_Name, Driver_Email, Driver_Phone, License_Number, License_Expiry, Availability_Status. Filters: License_Expiry, Availability_Status. Sort License_Expiry ascending. Profiles intended: Transport_Manager full.

Workflows: none beyond declarative validation/defaults.

**Implementation notes:** Driver_Email must be unique because Driver profile reports/workflows match logged-in driver using zoho.loginuserid. Avoid composite name fields; use simple text for robust matching.

## Vehicles

Maintain the college fleet with vehicle type, capacity, compliance dates, and availability. These records are used when assigning vehicles to approved trips.

Create one form: Vehicles.

Form: Vehicles
- Display name: Vehicles.
- Fields:
  - Section: Vehicle_Information, type=section, first field, row 1 column 0.
  - Vehicle_Number, type=text, must have, unique, display name Vehicle Number.
  - Vehicle_Type, type=picklist, must have, values: Bus, Van, Car, Jeep, Tempo Traveller, Other; display name Vehicle Type.
  - Seating_Capacity, type=number, must have, display name Seating Capacity.
  - Fuel_Type, type=picklist, values: Diesel, Petrol, CNG, Electric, Hybrid, Other; display name Fuel Type.
  - Registration_Expiry, type=date, display name Registration Expiry.
  - Insurance_Expiry, type=date, display name Insurance Expiry.
  - Fitness_Certificate_Expiry, type=date, display name Fitness Certificate Expiry.
  - Active_Status, type=picklist, must have, values: Active, Inactive; default/initial Active.
  - Availability_Status, type=picklist, must have, values: Available, Assigned, Maintenance, Inactive; default/initial Available.
  - Current_Odometer, type=number, display name Current Odometer.
  - Notes, type=textarea.
- Actions: standard Submit/Reset on add and Update/Cancel on edit.

Reports:
1. All_Vehicles — default list report from Vehicles. Columns: Vehicle_Number, Vehicle_Type, Seating_Capacity, Fuel_Type, Registration_Expiry, Insurance_Expiry, Fitness_Certificate_Expiry, Active_Status, Availability_Status, Current_Odometer. Filters: Vehicle_Type, Active_Status, Availability_Status. Sort Vehicle_Number ascending. Profiles intended: Transport_Manager full, Department_Manager read-only.
2. Available_Vehicles — list report from Vehicles where Active_Status == Active && Availability_Status == Available. Columns: Vehicle_Number, Vehicle_Type, Seating_Capacity, Fuel_Type, Availability_Status. Filters: Vehicle_Type, Seating_Capacity. Sort Vehicle_Type ascending, Vehicle_Number ascending. Profiles intended: Transport_Manager full.
3. Vehicle_Compliance_Expiry — list report from Vehicles where Active_Status == Active. Columns: Vehicle_Number, Vehicle_Type, Registration_Expiry, Insurance_Expiry, Fitness_Certificate_Expiry, Availability_Status. Filters: Registration_Expiry, Insurance_Expiry, Fitness_Certificate_Expiry. Sort Insurance_Expiry ascending. Profiles intended: Transport_Manager full.

Workflows: none beyond declarative validation/defaults.

**Implementation notes:** Vehicle_Number must be unique. Use picklists for type/fuel/status values to avoid inconsistent data.

## Transport_Requests

Capture staff transport requests and manage the full lifecycle from pending review to approval, assignment, and completion. Notifications and availability updates happen as the request moves between stages.

Create one form: Transport_Requests.

Form: Transport_Requests
- Display name: Transport Requests.
- Form-level: record owner = Added_User if supported for the form; success message confirming the request was submitted/updated.
- Fields:
  - Section: Request_Details, type=section, first field, row 1 column 0.
  - Request_Number, type=autonumber, start index 1000, display name Request Number.
  - Requester, type=picklist lookup to Staff_Directory.ID, displayformat Staff_Name, display name Requester.
  - Requester_Email, type=email, display name Requester Email.
  - Department, type=picklist lookup to Departments.ID, displayformat Department_Name, display name Department.
  - Request_DateTime, type=datetime, display name Request Date/Time, initial/default current date-time if valid syntax is available; otherwise set in on load.
  - Travel_Start, type=datetime, must have, display name Travel Start.
  - Travel_End, type=datetime, must have, display name Travel End.
  - Destination, type=text, must have, display name Destination.
  - Pickup_Location, type=text, must have, display name Pickup Location.
  - Passenger_Count, type=number, must have, display name Passenger Count.
  - Preferred_Vehicle_Type, type=picklist, values: Bus, Van, Car, Jeep, Tempo Traveller, Other; display name Preferred Vehicle Type.
  - Purpose, type=textarea, must have, display name Purpose of Travel.
  - Additional_Requirements, type=textarea, display name Additional Requirements.
  - Section: Approval_and_Assignment, type=section, row 2 column 1, visibility true.
  - Request_Status, type=picklist, must have, values: Pending, Approved, Rejected, Vehicle Assigned, Completed; initial/default Pending; this is the blueprint stage field.
  - Manager_Remarks, type=textarea, display name Manager Remarks.
  - Approval_DateTime, type=datetime, display name Approval Date/Time.
  - Approved_By_Email, type=email, display name Approved By Email.
  - Assigned_Vehicle, type=picklist lookup to Vehicles.ID, displayformat Vehicle_Number, display name Assigned Vehicle.
  - Assigned_Driver, type=picklist lookup to Drivers.ID, displayformat Driver_Name, display name Assigned Driver.
  - Assignment_DateTime, type=datetime, display name Assignment Date/Time.
  - Assignment_Remarks, type=textarea, display name Assignment Remarks.
  - Section: Driver_and_Completion, type=section, row 3 column 1, visibility true.
  - Driver_Acknowledgement, type=picklist, values: Pending, Acknowledged, Unable To Serve; initial/default Pending.
  - Driver_Remarks, type=textarea, display name Driver Remarks.
  - Completion_Remarks, type=textarea, display name Completion Remarks.
  - Completed_By_Email, type=email, display name Completed By Email.
  - Completed_DateTime, type=datetime, display name Completed Date/Time.
  - Approval_Notification_Sent, type=checkbox, internal flag, initial/default false.
  - Rejection_Notification_Sent, type=checkbox, internal flag, initial/default false.
  - Assignment_Notification_Sent, type=checkbox, internal flag, initial/default false.
  - Completion_Notification_Sent, type=checkbox, internal flag, initial/default false.
- Actions: standard Submit/Reset on add and Update/Cancel on edit.
- Blueprint components: stages exactly Pending, Approved, Rejected, Vehicle Assigned, Completed.

Blueprint workflow:
- Name: Transport_Request_Lifecycle.
- Form: Transport_Requests.
- Start stage: Pending.
- Stages: Pending, Approved, Rejected, Vehicle Assigned, Completed.
- Transitions:
  1. Submit Request: initial/create to Pending; owner Staff.
  2. Approve Request: Pending to Approved; owner Transport_Manager; requires Manager_Remarks; sets Approval_DateTime and Approved_By_Email.
  3. Reject Request: Pending to Rejected; owner Transport_Manager; requires Manager_Remarks; sets Approval_DateTime and Approved_By_Email.
  4. Assign Vehicle and Driver: Approved to Vehicle Assigned; owner Transport_Manager; requires Assigned_Vehicle, Assigned_Driver, Assignment_Remarks; sets Assignment_DateTime.
  5. Mark Completed: Vehicle Assigned to Completed; owners Driver and Transport_Manager; requires Completion_Remarks; sets Completed_By_Email and Completed_DateTime.

Form workflows:
1. Transport_Requests_On_Load — Trigger: on load. Actions: if adding a request as Staff, fetch Staff_Directory where Email == zoho.loginuserid and Active_Status == Active, then prefill Requester, Requester_Email, Department, Request_DateTime, Request_Status Pending, Driver_Acknowledgement Pending; hide/disable approval, assignment, notification flag, and completion fields for Staff; for Transport_Manager show approval/assignment fields; for Driver show only acknowledgement/completion fields relevant to assigned trips. Use field permissions for security and this workflow only for browser convenience/dynamic state.
2. Travel_Start_On_User_Input — Trigger: on user input/on update of Travel_Start. Actions: alert if Travel_Start is in the past or after Travel_End when Travel_End is present.
3. Travel_End_On_User_Input — Trigger: on user input/on update of Travel_End. Actions: alert if Travel_End is before Travel_Start.
4. Transport_Requests_On_Validate — Trigger: on add and on edit validate. Rules: Travel_End must be after Travel_Start; Passenger_Count must be greater than 0; Requester_Email must be present; if Request_Status is Approved or Rejected then Manager_Remarks is required; if Request_Status is Vehicle Assigned then Assigned_Vehicle and Assigned_Driver are required and must be active/available and vehicle capacity must be >= Passenger_Count; prevent overlapping non-completed/non-rejected bookings for the same vehicle or driver during the Travel_Start/Travel_End window; if Request_Status is Completed then Completion_Remarks is required.
5. Transport_Requests_On_Success — Trigger: on add success and on edit success. On add, email all active Transport_Team records where Can_Approve == true about the new pending request. On edit, send email notifications with flag guards: approved/rejected notification to Requester_Email when status changes to Approved/Rejected; assignment notification to Requester_Email and Assigned_Driver.Driver_Email when status becomes Vehicle Assigned; completion notification to Requester_Email and active transport approvers when status becomes Completed. When status becomes Vehicle Assigned, update Assigned_Vehicle.Availability_Status to Assigned and Assigned_Driver.Availability_Status to Assigned. When status becomes Completed, update assigned vehicle/driver back to Available.
6. Driver_Acknowledgement_On_User_Input — Trigger: on user input/on update of Driver_Acknowledgement. Actions: when Driver selects Unable To Serve require Driver_Remarks via alert and guide user; when Acknowledged, optionally set Driver_Remarks guidance.

Report workflows:
1. Mark_Completed — report button workflow for custom action Mark Completed. Triggered from assigned-trip reports for each record. If logged-in user is the assigned driver or Transport_Manager, set Request_Status to Completed, Completed_By_Email to zoho.loginuserid, Completed_DateTime to current date-time, and set a default completion remark when blank; then rely on on-success completion notification/availability update.

Reports:
1. All_Transport_Requests — default list report from Transport_Requests. Columns: Request_Number, Requester, Requester_Email, Department, Request_DateTime, Travel_Start, Travel_End, Destination, Passenger_Count, Preferred_Vehicle_Type, Request_Status, Assigned_Vehicle, Assigned_Driver, Approval_DateTime, Assignment_DateTime, Completed_DateTime. Filters: Department, Request_Status, Travel_Start, Assigned_Vehicle, Assigned_Driver. Sort Request_DateTime descending. Profiles: Transport_Manager full, Department_Manager read-only.
2. My_Transport_Requests — list report from Transport_Requests filtered to Requester_Email == zoho.loginuserid. Columns: Request_Number, Department, Request_DateTime, Travel_Start, Travel_End, Destination, Passenger_Count, Request_Status, Manager_Remarks, Assigned_Vehicle, Assigned_Driver, Assignment_Remarks, Completed_DateTime. Filters: Request_Status, Travel_Start. Sort Request_DateTime descending. Profiles: Staff.
3. Pending_Transport_Approvals — list report where Request_Status == Pending. Columns: Request_Number, Requester, Department, Request_DateTime, Travel_Start, Travel_End, Destination, Passenger_Count, Preferred_Vehicle_Type, Purpose, Request_Status. Filters: Department, Travel_Start, Preferred_Vehicle_Type. Sort Travel_Start ascending. Profiles: Transport_Manager.
4. Approved_For_Assignment — list report where Request_Status == Approved. Columns: Request_Number, Requester, Department, Travel_Start, Travel_End, Destination, Passenger_Count, Preferred_Vehicle_Type, Manager_Remarks, Request_Status. Filters: Department, Travel_Start, Preferred_Vehicle_Type. Sort Travel_Start ascending. Profiles: Transport_Manager.
5. Assigned_Trips — list report where Request_Status == Vehicle Assigned. Columns: Request_Number, Requester, Department, Travel_Start, Travel_End, Destination, Pickup_Location, Passenger_Count, Assigned_Vehicle, Assigned_Driver, Assignment_Remarks, Driver_Acknowledgement, Request_Status. Filters: Assigned_Vehicle, Assigned_Driver, Travel_Start, Driver_Acknowledgement. Sort Travel_Start ascending. Add per-record custom action "Mark Completed" that invokes Mark_Completed and is visible per record. Profiles: Transport_Manager.
6. Driver_My_Trips — list report filtered to Assigned_Driver.Driver_Email == zoho.loginuserid and Request_Status == Vehicle Assigned. Columns: Request_Number, Travel_Start, Travel_End, Destination, Pickup_Location, Passenger_Count, Assigned_Vehicle, Assignment_Remarks, Driver_Acknowledgement, Driver_Remarks, Request_Status. Filters: Travel_Start, Driver_Acknowledgement. Sort Travel_Start ascending. Add per-record custom action "Mark Completed" invoking Mark_Completed and visible per record. Profiles: Driver.
7. Completed_Trips — list report where Request_Status == Completed. Columns: Request_Number, Requester, Department, Travel_Start, Travel_End, Destination, Assigned_Vehicle, Assigned_Driver, Completed_By_Email, Completed_DateTime, Completion_Remarks. Filters: Department, Assigned_Vehicle, Assigned_Driver, Travel_Start. Sort Completed_DateTime descending. Profiles: Transport_Manager, Department_Manager.
8. Transport_Status_Board — kanban report from Transport_Requests grouped by Request_Status. Columns: Request_Number, Requester, Department, Travel_Start, Destination, Assigned_Vehicle, Assigned_Driver. Filters: Department, Travel_Start, Assigned_Driver. Profiles: Transport_Manager, Department_Manager.
9. Trip_Calendar — calendar report from Transport_Requests excluding Rejected. Columns: Request_Number, Requester, Department, Travel_Start, Travel_End, Destination, Assigned_Vehicle, Assigned_Driver, Request_Status. Calendar display field Request_Number; start date Travel_Start; end date Travel_End; default current month. Profiles: Transport_Manager, Department_Manager, Driver read-only for assigned trips if criteria/permissions can support it.

**Implementation notes:** Depends on Departments, Staff_Directory, Transport_Team, Vehicles, and Drivers. Implement the stage process using blueprint components and a blueprint workflow because this is a lifecycle/stage-based process. Use profile field permissions for security, and on-load/on-user-input workflows only for dynamic prefilling/locking/availability hints.

## Transport_Dashboard

Create a management dashboard for current request volumes, fleet availability, upcoming trips, and status distribution. This gives transport managers and college management a quick operational view.

Create one dashboard page: Transport_Dashboard.

Page: Transport_Dashboard
- Display name: Transport Dashboard.
- Audience: Transport_Manager and Department_Manager; Staff/Driver do not need dashboard access unless permissions later allow read-only.
- Build with a rich HTML snippet-first layout, using .dshtml and/or .zml snippets. Prefer ZCS themed components for cards, badges, buttons, tables, and charts where possible.
- Components/content to include:
  1. KPI cards: Pending Requests, Approved Awaiting Assignment, Assigned Trips, Completed Trips This Month, Available Vehicles, Available Drivers.
  2. Status distribution visual: simple CSS bar/donut style or ZCS chart-like cards based on counts of Request_Status.
  3. Upcoming trips table for the next 7 days showing request number, department, travel start/end, destination, assigned vehicle, assigned driver, and status.
  4. Fleet availability section with cards for vehicle statuses: Available, Assigned, Maintenance, Inactive.
  5. Driver availability section with counts for Available, Assigned, On Leave, Inactive.
  6. Quick links/buttons to Pending_Transport_Approvals, Approved_For_Assignment, Assigned_Trips, Available_Vehicles, and Available_Drivers reports.
- Use inline Deluge inside snippets to compute counts by querying Transport_Requests, Vehicles, and Drivers.
- Avoid JavaScript. HTML/CSS and Deluge only.
- Main page must reference snippets through <file name:.../> placeholders according to page docs.
- Do not add menu mappings here; UI Configuration segment handles menus.

**Implementation notes:** Prefer .dshtml and/or .zml snippets over native page components. Use ZCS components where useful and include shared ZCS global CSS if used. Main page file must be Pages/Transport_Dashboard.ds; snippets under Pages/Transport_Dashboard/.

## Permissions

Add complete permissions for every profile after all forms, reports, and pages exist. This locks down requester, manager, transport, and driver access appropriately.

Edit custom profile files under Permissions/Profiles/ to add complete ModulePermissions for all forms, reports, and the Transport_Dashboard page. Do not create roles unless explicitly required later; this app uses profile permissions plus report criteria for practical access separation.

Profiles and intended permissions:

1. Staff
- Departments: read-only access to Active_Departments; no create/update/delete.
- Staff_Directory: read-only access to active staff fields needed for requester lookup; no create/update/delete.
- Transport_Team, Drivers, Vehicles: no direct master maintenance; Vehicles/Drivers assignment details visible only through My_Transport_Requests fields after assignment.
- Transport_Requests: create allowed; update allowed only where platform/report access permits their own editable request records; delete disabled. Field permissions: editable for request details before/internal workflow restrictions; read-only for Request_Number, Request_DateTime after set, Request_Status, Manager_Remarks, Assigned_Vehicle, Assigned_Driver, Assignment_Remarks, Driver_Acknowledgement, Completed_By_Email, Completed_DateTime; hidden for approval notification flags and internal email flags; no edit to approval/assignment/completion fields.
- Reports: My_Transport_Requests only, plus any embedded self-service request report if created. No access to all/pending/assignment reports.
- Pages: no Transport_Dashboard access.

2. Department_Manager
- Read-only oversight. No create/update/delete on master or transaction forms.
- Departments, Staff_Directory, Vehicles, Transport_Requests: read-only fields relevant to oversight. Hide notification flag fields.
- Reports: All_Departments, Active_Departments, Active_Staff_By_Department, All_Vehicles, All_Transport_Requests, Completed_Trips, Transport_Status_Board, Trip_Calendar. No access to Pending approval edit/action reports unless read-only can be safely enforced.
- Pages: read-only access to Transport_Dashboard.

3. Transport_Manager
- Full create/read/update/delete for Departments, Staff_Directory, Transport_Team, Drivers, Vehicles where appropriate.
- Transport_Requests: full create/read/update; delete can be enabled only for administrative cleanup; full field visibility except notification flags may be visible read-only or hidden per best practice. Can approve/reject/assign/complete. Can use Mark Completed action.
- Reports: all reports for all forms, including Pending_Transport_Approvals, Approved_For_Assignment, Assigned_Trips, Transport_Status_Board, Trip_Calendar, dashboard.
- Pages: full access to Transport_Dashboard.

4. Driver
- Drivers: read-only access to own driver-facing identity fields if profile/report criteria can restrict; otherwise no direct master report except Driver_My_Trips.
- Transport_Requests: read-only for assigned trip details; update allowed only for Driver_Acknowledgement, Driver_Remarks, Completion_Remarks, Completed_By_Email, Completed_DateTime/Mark Completed action where platform supports field-level update. Hide requester email if not necessary, approval remarks only read-only if relevant, all notification flags hidden.
- Reports: Driver_My_Trips and Trip_Calendar if criteria can limit to assigned driver; no access to all/pending/approved reports.
- Pages: no Transport_Dashboard access.

Permissions must include FieldPermissions for every field in each form and ReportPermissions for every report generated. Include PagePermissions for Transport_Dashboard if page permission syntax is supported by the profile docs.

**Implementation notes:** Edit the shell profile files created in the User Profiles segment. Read all generated form/report/page files before writing permissions so FieldPermissions and ReportPermissions match actual link names.

## UI Configuration

Configure forms, navigation, visual preferences, and report layouts for web and mobile usage. This makes every form/report reachable and ensures key transport workflows are usable on phones.

Create UI and device configuration for all generated forms/reports/pages.

Web form mappings:
- UI/web/forms.ds: include all forms with consistent label placement: Departments, Staff_Directory, Transport_Team, Drivers, Vehicles, Transport_Requests.

Web menu:
- UI/web/menu.ds with spaces/sections:
  1. Dashboard: page Transport_Dashboard.
  2. Requests: form/report entries for Transport_Requests, My_Transport_Requests, Pending_Transport_Approvals, Approved_For_Assignment, Assigned_Trips, Completed_Trips, Transport_Status_Board, Trip_Calendar.
  3. Fleet Masters: Vehicles reports, Drivers reports.
  4. People & Teams: Departments, Staff_Directory, Transport_Team reports.
  5. SharedAnalytics_Section: mandatory shared user report section.
- Use valid icons from icons docs, favor transportation, education, users, and business icons.

Customize:
- UI/web/customize.ds: set clean college transport theme preferences: readable font, neutral background, primary color suitable for transport/education, and log preferences if required by syntax.
- UI/phone/menu.ds and UI/phone/customize.ds: include mobile-focused navigation for My_Transport_Requests, Driver_My_Trips, Assigned_Trips, Trip_Calendar, and Transport_Dashboard for managers if practical.
- UI/tablet/menu.ds and UI/tablet/customize.ds only if supported/needed; otherwise web plus phone is enough.

DeviceUI report layouts:
- Create Components/<FormName>/Reports/DeviceUI/web_<ReportName>.ds for EVERY report listed below, no exceptions.
- Create phone_<ReportName>.ds for the mobile-critical reports: My_Transport_Requests, Driver_My_Trips, Assigned_Trips, Pending_Transport_Approvals, Approved_For_Assignment, Trip_Calendar.
- Tablet variants optional unless menu surfaces reports on tablet.
- Each DeviceUI file must define quickview and detailview layouts using only fields present in the parent report's show all rows from column list.
- If a report has custom action "Mark Completed" with show action for each record = true, include "Mark Completed" in the fields block of both quickview and detailview.

Reports requiring web DeviceUI:
Departments: All_Departments, Active_Departments.
Staff_Directory: All_Staff, Active_Staff_By_Department.
Transport_Team: All_Transport_Team, Active_Approvers.
Drivers: All_Drivers, Available_Drivers, Driver_License_Expiry.
Vehicles: All_Vehicles, Available_Vehicles, Vehicle_Compliance_Expiry.
Transport_Requests: All_Transport_Requests, My_Transport_Requests, Pending_Transport_Approvals, Approved_For_Assignment, Assigned_Trips, Driver_My_Trips, Completed_Trips, Transport_Status_Board, Trip_Calendar.

**Implementation notes:** Mandatory: emit a web DeviceUI file for every report in the app. For reports with per-record custom action "Mark Completed", include the quoted action name in quickview/detailview fields. Verify every DeviceUI field exists in the parent report definition.