## Application Overview
This Zoho Creator build adds an ad-hoc transport management module for colleges, enabling staff to request vehicles, transport managers to approve or reject requests, and the transport office to assign vehicles and drivers. It tracks each trip from request submission through approval, assignment, and completion with email notifications for requesters, approvers, and drivers.

## Forms
| Form Name | Purpose | Key Lookups |
|---|---|---|
| Departments | Maintain college department master data | None |
| Staff_Directory | Maintain staff requester directory | Departments |
| Transport_Team | Maintain transport approvers/coordinators | None |
| Drivers | Maintain driver master, license, and availability | None |
| Vehicles | Maintain fleet, capacity, compliance, and availability | None |
| Transport_Requests | Capture travel requests and trip lifecycle details | Staff_Directory, Departments, Vehicles, Drivers |

## Reports
| Report Name | Type | Source Form |
|---|---|---|
| All_Departments, Active_Departments | List | Departments |
| All_Staff_Directory, Active_Staff_By_Department | List | Staff_Directory |
| All_Transport_Team, Active_Approvers | List | Transport_Team |
| All_Drivers, Available_Drivers, Driver_License_Expiry | List | Drivers |
| All_Vehicles, Available_Vehicles, Vehicle_Compliance_Expiry | List | Vehicles |
| All_Transport_Requests, My_Transport_Requests, Pending_Transport_Approvals, Approved_For_Assignment, Assigned_Trips, Driver_My_Trips, Completed_Trips | List | Transport_Requests |
| Transport_Status_Board | Kanban | Transport_Requests |
| Trip_Calendar | Calendar | Transport_Requests |

## Pages
| Page Name | Purpose | Key Components |
|---|---|---|
| Transport_Dashboard | Transport operations overview for managers | KPI cards, status distribution, upcoming trips, fleet/driver availability, quick links |

## Design Decisions
- Lifecycle actions use report buttons/workflows instead of blueprints, per requirement.
- Staff, transport managers, drivers, and department managers have separate custom profiles.
- Vehicle/driver availability is updated during assignment and completion workflows.
- Web quick/detail layouts were added for every transport report; mobile layouts focus on requests, approvals, assignments, driver trips, and calendar.
- Existing academic components were preserved and the transport menu was added as a separate space.
