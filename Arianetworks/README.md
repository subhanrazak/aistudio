## Application Overview
Aria Networks PLM governs item masters, hybrid BOMs, NIR gating, engineering/manufacturing changes, deviations, ECN acknowledgments, and audit history. It uses profile-aware approvals, shared automation functions, and custom analysis pages for PLM teams.

## Forms
| Form Name | Purpose | Key Lookups |
|---|---|---|
| Employee_Master | Employee directory/routing identity | Creator user |
| Category_Master | APN category and prefix rules | — |
| Manufacturer_Master | Approved manufacturer data | — |
| Approval_Matrix_Template | Default approval routes | Employee_Master |
| Notification_Template | Internal email templates | — |
| System_Config | Global PLM settings | — |
| Item_Master | Items, lifecycle, revisions, alternates, BOM grid | Category, Manufacturer, Employee, BOM_Line, NIR |
| BOM_Line | Parent-child BOM rows | Item_Master |
| New_Item_Request | Engineer item creation gate | Category, Employee, Manufacturer |
| Change_Request | ECR/MCR intake and triage | Employee, affected-item rows |
| Change_Order | ECO/MCO/PCO/Deviation approval and release | Change_Request, Employee, affected/disposition/approval rows |
| Approval_Remarks | Approver decisions/comments | Change_Order, Employee |
| Deviation_Consumption_Entry | Deviation unit consumption | Change_Order, Employee |
| ECN_Acknowledgment | Internal ECN acknowledgments | Change_Order, Employee |
| Activity_Log | System audit trail | Employee |
| Supporting subforms | Affected items, dispositions, approvals, subscriptions, history | Item_Master, Change_Order |

## Reports
| Report Name | Type | Source Form |
|---|---|---|
| All_Items / My_Working_Items | List | Item_Master |
| Items_By_Lifecycle | Kanban | Item_Master |
| Where_Used | List | BOM_Line |
| My_NIRs / All_Open_NIRs | List | New_Item_Request |
| My_Requests / All_Open_Requests | List | Change_Request |
| All_Change_Orders / My_Pending_Approvals | List | Change_Order |
| Change_Orders_By_Status | Kanban | Change_Order |
| Open_Deviations_Calendar | Calendar | Change_Order |
| Audit_History | List | Activity_Log |
| Master/config reports | List | Employee/category/manufacturer/config forms |
| Operational logs | List | Approval, deviation, ECN, subscription, revision forms |

## Pages
| Page Name | Purpose | Key Components |
|---|---|---|
| PLM_Dashboard_Home | Role-aware landing dashboard | KPI cards, charts, queues, activity |
| BOM_Browser | Multi-level BOM tree | HTML tree snippet |
| BOM_Flatten_Page | Aggregated procurement BOM | Export table |
| Where_Used_Explorer | Direct/indirect impact analysis | Recursive tables |
| BOM_Redline_Viewer | Visual BOM change review | Redline table |
| BOM_Compare | Assembly/variant comparison | Side-by-side table |
| BOM_Bulk_Remove | Controlled removal planning | Selection/instruction UI |
| Change_Order_Summary | CO status and approver summary | Status bar, error panels |
| Item_Sourcing_View | Manufacturer/MPN sourcing | Flattened sourcing tables |
| Item_Revision_Snapshot_View | Revision snapshot rendering | Snapshot detail table |

## Design Decisions
- Custom profiles are declared first, then permissions converge after components exist.
- APNs are data-driven from Category_Master prefixes.
- Engineers create normal items only through approved NIRs.
- Released item/BOM changes flow through Change Orders; deletions are soft/redline-based.
- ECNs are internal-only; manufacturer contacts are reference data.