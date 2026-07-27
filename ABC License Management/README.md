## Application Overview
ABC License Management is a Zoho Creator application for public licensing intake, renewals, payments, enforcement casework, correspondence, and audit tracking. It provides portal-facing self-service, staff action centers, lifecycle buttons on operational queues, role-based permissions, and web/mobile device layouts.

## Forms
| Form Name | Purpose | Key Lookups |
|---|---|---|
| Applicant_Profile | Applicant/contact profile | — |
| Applications | Guided new-license intake and review | Applicant_Profile, DBA, License, Issued_License |
| Licenses | Issued-license lifecycle and renewal status | License_Type, Entities, Premises, Applications |
| Renewal_Batches / Renewal_Items / Renewal_Notices | Renewal notice, payment, and completion tracking | Licenses, Payments |
| Payments | Fee payment, refund, and reconciliation tracking | Applications, Licenses, Renewal_Batches |
| Complaints / Cases / Violations / Evidence | Enforcement screening, investigations, legal review, and evidence | Licenses, Entities, Premises, Add_Agents |
| Correspondence / Audit_Log | Notices, documents, signatures, and audit events | Source module records |
| Reference/Master Forms | License types, application types, users, addresses, attorneys, DBAs | Shared reference data |

## Reports
| Report Name | Type | Source Form |
|---|---|---|
| All_Applications, Staff_Application_Queue, New_License_Application_Queue, Investigator_Review_Queue | List | Applications |
| Application_Status_Board, License_Status_Board, Case_Status_Board | Kanban | Applications / Licenses / Cases |
| All_Licenses, Active_Licenses, Renewable_Licenses, Licensee_Portal_Licenses | List | Licenses |
| All_Renewal_Batches, Renewal_Payment_Queue, Licensee_Renewal_Batches | List | Renewal_Batches |
| All_Payments, Pending_Payments, Refund_Queue, Daily_Reconciliation | List | Payments |
| Enforcement_Work_Queue, Supervisor_Screening_Queue, Legal_Review_View, Evidence_Register | List | Enforcement forms |
| Correspondence_Log, Pending_Correspondence, Signed_Documents, Enforcement_Documents | List | Correspondence |

## Pages
| Page Name | Purpose | Key Components |
|---|---|---|
| Public_Applicant_Action_Center | Applicant to-do workspace | HTML KPI cards, owned queues, wizard links |
| Public_Application_Wizard | Multi-step application intake | Typed parameters, step navigation, embedded Applications form |
| Licensee_Action_Center | Licensee renewal/payment workspace | KPI cards, renewal/license queues, action links |
| Licensing_Staff_Action_Center / Licensing_Supervisor_Action_Center | Licensing operational workspaces | Queue cards, bottleneck tables, report links |
| Accounting_Staff_Action_Center | Payment/refund/reconciliation workspace | Payment KPIs, queue tables, action links |
| Enforcement_Agent_Action_Center / Enforcement_Supervisor_Action_Center / OLS_Attorney_Action_Center | Enforcement and legal workspaces | Case, complaint, evidence, legal-review sections |
| Public_Application_Portal, Renewal_Portal, Licensing_Operations_Dashboard, Enforcement_Command_Center | Existing portal/dashboard pages | HTML snippets, KPIs, summaries |

## Design Decisions
- Action buttons were added to report queues so users can progress work without opening full records.
- Login identity logic uses `zoho.loginuserid` for email-based filtering and audit capture.
- The public application wizard uses helper fields and form workflows to show one intake step at a time.
- DeviceUI files include visible custom actions so web/mobile report layouts expose the new buttons.