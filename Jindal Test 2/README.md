## Application Overview
Annual FY budget planning app for Sales, Operations, SCM/PPC, Sourcing, Finance, Management, and Audit. Finance opens cycles, Sales submits demand, Operations validates availability/production, SCM reviews feasibility/revisions, and Finance completes the final budget.

## Forms
| Form Name | Purpose | Key Lookups |
|---|---|---|
| Financial_Years | FY anchor/completion | — |
| Financial_Year_Months | Configurable FY months | Financial_Years |
| Budget_Cycles | Master stage tracker | Financial_Years, Budget_Cycles |
| Market_Segments | Grade master | — |
| Steel_Grades | Product/Series master | — |
| Sales_Plans | FY demand and product split | FY, Cycle, Grades, Products |
| Capacity_TEP_Plans | Operations line availability | FY, Cycle, Plant, Line, Months |
| Operations_Production_Plans | Product/month production tons | FY, Cycle, Plant, Line, Availability, Products |
| Raw_Material_Budgets | RM availability, need, cost | FY, Cycle, Plant, Raw_Materials |
| Volume_Consolidations | SCM review gate | FY, Cycle, Sales, Operations |
| Replanning_Requests | Revision-copy history | Cycle, FY |
| Financial_Consolidations | Final finance consolidation | FY, Cycle, SCM Review |
| Approval_Audit_Log | Approval/revision audit | Cycle |

## Reports
| Report Name | Type | Source Form |
|---|---|---|
| Financial year and month views | List | Financial_Years, Financial_Year_Months |
| Cycle active/status/locked/completed views | List/Kanban | Budget_Cycles |
| Grade and product master views | List | Market_Segments, Steel_Grades |
| Sales workqueues, approvals, status board | List/Kanban | Sales_Plans |
| Operations availability/production views | List/Kanban | Capacity_TEP_Plans, Operations_Production_Plans |
| RM budget and SCM availability views | List | Raw_Material_Budgets |
| SCM ready, revision, finalised, shortfall views | List/Kanban | Volume_Consolidations |
| Replanning status/history views | List/Kanban | Replanning_Requests |
| Financial summary/status/final budget views | List/Kanban | Financial_Consolidations |
| Audit by cycle and critical events | List | Approval_Audit_Log |

## Pages
| Page Name | Purpose | Key Components |
|---|---|---|
| Operations_Landing | Operations overview | KPIs, availability matrix, production matrix, reports |
| SCM_Landing | SCM review workbench | KPIs, review matrix, revision history, queues |
| Planning_Workbench | Department task hub | Task cards, queue grid, reports, guidance |
| Executive_Budget_Dashboard | Management visibility | KPIs, bottlenecks, plant matrix, exceptions |
| Scenario_Comparison_Dashboard | Scenario comparison | Cards, variance bars, decision panel |
| Finance/Executive/Audit/Plant landings | Role landing pages | Focused snippets and links |

## Design Decisions
- FY-level Sales planning replaces monthly/quarterly entry.
- Operations uses configurable month rows, not fixed Apr–Mar fields.
- Existing link names remain for Grades and Products to protect data.
- Approvals use form-save workflows, avoiding custom report buttons.
- SCM is gated until Sales and Operations approvals are complete.