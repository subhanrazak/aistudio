## Application Overview
IITB FMS manages vendor attendance, invoices, consumables, warnings/penalties, assets, and maintenance. Infra, F&A, vendor, and admin users get role-focused dashboards with audited approvals.

## Forms
| Form Name | Purpose | Key Lookups |
|---|---|---|
| User_Master | Users/vendors directory | — |
| Email_Template | Notification templates | — |
| Audit_Log | Audit trail | — |
| Action_Capture | Button action capture | — |
| FMS_Employee_Master | Vendor employees | Vendor |
| Warning_Penalty_Type_Master | Warning/penalty setup | — |
| Asset_Category_Master | Asset categories | — |
| Consumable_Category_Master | Consumable categories | — |
| Consumable_Item_Master | Consumable items/rates | Category |
| Attendance_Submission | Attendance submission flow | Vendor |
| Attendance_Invoice | Attendance invoice flow | Vendor, Submission |
| Attendance_Record | Daily attendance | Employee, Vendor |
| Consumable_Invoice | Consumable invoice flow | Vendor, Items |
| Warning_Penalty | Warning/disciplinary cases | Vendor, Employee, Type |
| Asset_Master | Asset register | Category, Vendor |
| Maintenance_Schedule_Configuration | PM schedule setup | Asset, Employee |
| Maintenance_Task | Maintenance jobs | Schedule, Asset |
| Maintenance_Task_History | Status trail | Maintenance_Task |

## Reports
| Report Name | Type | Source Form |
|---|---|---|
| Vendor_Master_List, User_Master_List | List | User_Master |
| Email_Template_List | List | Email_Template |
| Audit_Log_List | List | Audit_Log |
| Attendance_Submission_* | List | Attendance_Submission |
| Attendance_Invoice_* | List | Attendance_Invoice |
| Attendance_Record_Admin_List | List | Attendance_Record |
| Consumable_Invoice_* | List | Consumable_Invoice |
| Warning_List_* | List | Warning_Penalty |
| Asset_Master_List_Infra, Asset_Reference_List_FMS | List | Asset_Master |
| Maintenance_Schedule_List_Infra | List | Maintenance_Schedule_Configuration |
| Maintenance_Task_* | List | Maintenance_Task |
| Maintenance_Task_History_Report | List | Maintenance_Task_History |
| Master setup lists | List | Setup forms |

## Pages
| Page Name | Purpose | Key Components |
|---|---|---|
| Home | Landing/routing hub | KPI cards, role links |
| Infra_Team_Dashboard | Infra queues | Embedded reports, KPIs |
| FA_Team_Dashboard | F&A queues | Embedded reports, audit view |
| FMS_Vendor_Dashboard | Vendor workspace | Embedded reports/forms |

## Design Decisions
- Pages are primary menu entries; reports/forms support embeds and permissions.
- Report actions handle approvals/rejections and audit entries.
- India defaults: Asia/Kolkata, `dd-MMM-yyyy`, 24-hour time.
- Web DeviceUI exists for every report; mobile/tablet cover key queues.
- Compile status: success, 0 errors, 0 warnings.
