## Application Overview
DX Training Team Internal manages training events, team task assignment, daily work updates, leave requests, post-event performance, discounts, invoices, QR codes, and public enquiry forms. The app now includes operational tracking for task due dates, blockers, workload, upcoming events, and daily update visibility.

## Forms
| Form Name | Purpose | Key Lookups |
|---|---|---|
| Events | Event master, schedule, survey tracking | Products, Team_Members |
| Event_Tasks | Assign event work and hours | Products, Events, Multiple_tasks_subform |
| Multiple_tasks_subform | Task assignment rows with priority, due date, hours, blocker status | Event_Tasks, Team_Members, General_Tasks |
| Task_Updates | Daily team work update submissions | Team_Members, Task_updates_subform1 |
| Team_Members | Team profile and user mapping | Team_Members self lookup, users |
| Post_Event_Stats | Registrations, attendance, revenue | Products, Events, child detail forms |
| Discounts_Request / Manual_Invoice | Promo codes and invoicing | Products, Events, Team_Members |

## Reports
| Report Name | Type | Source Form |
|---|---|---|
| Upcoming_Events_30_Days | List | Events |
| Events_Needing_Task_Plan / Events_Needing_Post_Event_Stats | List | Events |
| My_Open_Task_Assignments / Overdue_Task_Assignments / Blocked_Task_Assignments | List | Multiple_tasks_subform |
| Task_Workload_By_Member | List | Multiple_tasks_subform |
| Todays_Task_Update_Rows / My_Task_Update_Rows / Completed_Task_Update_Rows | List | Task_updates_subform1 |
| Recent_Daily_Update_Submissions | List | Task_Updates |
| Core imported reports | List/calendar/custom | Existing forms |

## Pages
| Page Name | Purpose | Key Components |
|---|---|---|
| Dashboard | Training metrics overview | KPI panels, stacked column, pie, donut charts |
| Operations_Dashboard | Daily operations and scheduling overview | KPI cards, embedded reports, task charts |

## Design Decisions
- Added task-level planning fields instead of replacing the existing daily-update flow.
- Added operational reports for upcoming events, overdue work, blockers, workload, and daily updates.
- Kept phone menu clean by mapping new web-only operational items under unused.
- Preserved imported workflows while adding lightweight scheduling and dashboard improvements.
