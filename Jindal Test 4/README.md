## Application Overview
This enhancement makes Volume Consolidation an all-plant SCM review flow instead of a single-plant check. Sales product mix is copied into the consolidation, Sales approves any product mix change first, and SCM performs the final review after Sales and/or Operations revisions are resolved.

## Forms
| Form Name | Purpose | Key Lookups |
|---|---|---|
| Volume_Consolidations | Parent all-plant SCM consolidation, product mix approval, revision loop, and final status tracking | Financial_Years, Budget_Cycles, Sales_Plans, Plants, Capacity_TEP_Plans, Operations_Production_Plans |
| Volume_Product_Mix_Lines | Child product mix rows copied from Sales Plan and reviewed by Sales/SCM | Market_Segments, Steel_Grades |
| SCM_Review_Lines | All-plant review matrix rows with plant, line, production, availability, and product-mix context | Plants, Production_Lines, Capacity_TEP_Plans, Operations_Production_Plans, Market_Segments, Steel_Grades, Raw_Materials |
| Revision_History_Lines | Audit trail for Sales, Operations, both-team, and SCM revision comments/outcomes | Embedded in Volume_Consolidations |

## Reports
| Report Name | Type | Source Form |
|---|---|---|
| Sales_Product_Mix_Approval_Queue | List | Volume_Consolidations |
| Operations_Revision_Queue | List | Volume_Consolidations |
| SCM_Ready_For_Review | List | Volume_Consolidations |
| SCM_Revision_Requests | List | Volume_Consolidations |
| All_Volume_Consolidations | List | Volume_Consolidations |
| Consolidation_Status_Board | Kanban | Volume_Consolidations |
| All_Volume_Product_Mix_Lines | List | Volume_Product_Mix_Lines |
| All_SCM_Review_Lines | List | SCM_Review_Lines |
| All_Revision_History_Lines | List | Revision_History_Lines |

## Pages
| Page Name | Purpose | Key Components |
|---|---|---|
| Sales_Management_Landing | Sales product mix approval workbench | KPI cards, queue table, approval guidance, queue link |
| SCM_Landing | All-plant SCM review workbench | KPI cards, all-plant matrix, revision timeline, queue links |
| Operations_Landing | Operations revision and all-plant feeder view | Revision KPIs, revision queue, all-plant feeder table, matrix guidance |

## Design Decisions
- One Volume Consolidation can represent all plants for a budget cycle.
- Product mix is copied from Sales Plan into a dedicated child grid.
- Sales approves product mix before SCM final approval.
- Sales/Operations/Both revision loops repeat through status fields and comments until SCM approves.
- Report buttons are kept as manual-wiring placeholders; form workflows process the actual actions.