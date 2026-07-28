## Application Overview
Travel & Expense Policy Compliance Checker is a Phase 1 Zoho Creator surround app for banking T&E control. It stages SAP FI-TV/HR data, checks claims against configurable policies, routes exceptions, and provides manager, compliance, finance, HR, and audit dashboards. SAP integration is represented with sync-log placeholders, not live credentials.

## Forms
| Form Name | Purpose | Key Lookups |
|---|---|---|
| TE_Employees | Employee/routing master | None |
| TE_Claims | Claim headers and scorecards | TE_Employees |
| TE_Line_Items | Expense line details | TE_Claims |
| TE_Compliance_Results | Rule check outcomes | TE_Claims, TE_Line_Items, TE_Policy_Rules |
| TE_Policy_Rules | Configurable rule catalog | None |
| TE_Rate_Tables | City/grade rates | None |
| TE_Distance_Lookups | Mileage route distances | None |
| TE_Holiday_Calendar | Holiday/weekend calendar | None |
| TE_Entertainment_Budgets | Executive entertainment caps | TE_Employees |
| TE_Exceptions | Exception approvals | TE_Claims, TE_Line_Items, TE_Compliance_Results |
| TE_Audit_Log | Audit trail | None |
| TE_Sync_Log | SAP sync placeholder history | None |

## Reports
| Report Name | Type | Source Form |
|---|---|---|
| Claim views: All, Pending, Red Flagged | List | TE_Claims |
| Claims_By_Status | Kanban | TE_Claims |
| Trip_Calendar | Calendar | TE_Claims |
| Line-item review views | List | TE_Line_Items |
| Scorecards and violation views | List | TE_Compliance_Results |
| Exception queues/history | List/Kanban | TE_Exceptions |
| Policy/rate maintenance views | List/Spreadsheet | TE_Policy_Rules, TE_Rate_Tables |
| Distance, holiday, budget views | List/Calendar/Spreadsheet | Master forms |
| Employee and repeat-offender views | List | TE_Employees |
| Audit and SAP sync views | List | TE_Audit_Log, TE_Sync_Log |

## Pages
| Page Name | Purpose | Key Components |
|---|---|---|
| Compliance_Dashboard | Executive KPIs | KPI cards, charts, heatmap, feeds |
| Manager_Approval_Queue | Manager review | Scorecards, approval report, SLA panel |
| My_Claims_Status | Claimant self-service | Status, violations, exception tracker |
| Rule_Configuration | Policy setup | Embedded reports/forms, audit feed |
| Exception_Management | Exception operations | Tier queues, SLA list, kanban, trends |
| Audit_Analytics | Audit package | Export reports, repeat offenders, sync health |

## Design Decisions
- Phase 1 uses SAP sync placeholders; no credentials/connectors.
- USD banking defaults with currency fields retained.
- Custom profiles plus roles model internal and portal access.
- All reports have web device layouts; key queues have mobile/tablet variants.