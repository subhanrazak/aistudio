## Application Overview
Zylker RiskQ is an ERM/Internal Audit application for planning audits, managing risk and control libraries, executing tests, tracking observations, remediation, and follow-ups. It includes role-based access, lifecycle workflows, and screen-inspired dashboards for audit, risk, planning, and follow-up analytics.

## Forms
| Form Name | Purpose | Key Lookups |
|---|---|---|
| Departments | Business units and risk ownership areas | Parent_Department |
| Audit_Team_Members | Auditors, managers, owners, approvers | Departments |
| Audit_Universe | Auditable entities and risk scores | Departments |
| Control_Library | Reusable controls | Departments, Audit_Team_Members |
| Risk_Register | Detailed enterprise risks | Departments, Audit_Universe, Audit_Team_Members |
| Workpaper_Templates | Audit workpaper guidance | Audit_Team_Members |
| Test_of_Controls_Library | Reusable control tests | Control_Library, Audit_Team_Members |
| Observation_Form_Templates | Observation form configuration | Audit_Team_Members |
| Audit_Plans | Risk-based audit plans | Departments, Audit_Team_Members |
| Audit_Plan_Entities | Plan-to-entity scheduling | Audit_Plans, Audit_Universe, Departments |
| Audits | Audit engagements | Departments, Audit_Plans, Audit_Team_Members |
| Audit_Test_Executions | Test execution results | Audits, Test_of_Controls_Library, Control_Library |
| Audit_Observations | Findings and observations | Audits, templates, tests, Departments |
| Remediation_Tasks | Action plans and closure | Audit_Observations, Departments, Audit_Team_Members |
| Follow_Ups | Follow-up monitoring | Audits, Observations, Departments, Audit_Team_Members |
| Add_Users | In-app user administration | Profiles |

## Reports
| Report Name | Type | Source Form |
|---|---|---|
| Master and risk profile views | list/kanban | Departments, Audit_Universe |
| Risk register views | list/calendar/kanban | Risk_Register |
| Library views by type/status | list/kanban | Controls, workpapers, tests, observation templates |
| Planning views by year/entity/quarter/skill | list/kanban | Audit_Plans, Audit_Plan_Entities |
| Execution calendars/boards/listings | list/calendar/kanban | Audits, Audit_Test_Executions, Audit_Observations |
| Task and follow-up trackers | list/calendar/kanban | Remediation_Tasks, Follow_Ups |
| All_Users | list | Add_Users |

## Pages
| Page Name | Purpose | Key Components |
|---|---|---|
| Internal_Audit_Dashboard | Audit command center | KPI cards, engagement cards, observation/follow-up/test tables |
| Risk_Register_Dashboard | Risk library/register view | KPI cards, filters, risk cards, residual-risk visuals |
| Audit_Planning_Workspace | Planning workspace | Stepper, plan KPIs, entity/quarter/skill tables |
| Follow_Up_Tracker_Dashboard | Follow-up analytics | KPIs, bar/line/donut/aging charts, summary tables |
| Audit_Dashboard | Legacy aligned dashboard | Summary KPI cards and links |

## Design Decisions
- One business form per domain keeps reports and permissions maintainable.
- Deluge handles multi-field validation and lifecycle stamping.
- Dashboards use HTML snippets for red/white screen-faithful layouts.
- Users module is included, with user management limited to administrator access.
- Legacy audit CRM-style modules were retained under Legacy navigation.