# Ather Energy Manufacturing Intelligence Platform

## Application Overview
A Zoho Creator app providing two integrated modules for Ather Energy's manufacturing operations: a **Headcount Calculation Tool (HCCT)** for real-time workforce gap analysis across production shifts, and a **DDMRP Buffer Engine** for demand-driven material requirements planning with automated daily buffer zone recalculation and supply alerts.

## Forms

| Form Name | Purpose | Key Lookups |
|---|---|---|
| Employee_Master | Employee records with role, shift, and status | — |
| Production_Plan | Weekly production targets per line/SKU | — |
| Shift_Configuration | Shift timing and available hours per line | — |
| Headcount_Calculator | Calculates required HC, gap, and utilisation | — |
| HC_Actual_Entry | Daily actual headcount attendance entry | — |
| Part_SKU_Master | Part/SKU master with ADU and lead time | — |
| Decoupling_Point_Master | DDMRP decoupling point parameters per part | → Part_SKU_Master |
| Buffer_Profile_Levels | Computed Red/Yellow/Green buffer zones per part | → Part_SKU_Master |
| Daily_Stock_Snapshot | Daily on-hand, on-order, and demand quantities | → Part_SKU_Master |
| NFP_Status_Log | Daily Net Flow Position status (RED/YELLOW/GREEN) | → Part_SKU_Master |
| Supply_Alert_Log | Alerts for RED-zone parts with acknowledgment | → Part_SKU_Master |

## Reports

| Report Name | Type | Source Form |
|---|---|---|
| All_Employees | List (default) | Employee_Master |
| Employees_By_Department | List (grouped) | Employee_Master |
| All_Production_Plans | List (default) | Production_Plan |
| Weekly_Production_Plans | List (grouped) | Production_Plan |
| All_Shifts | List (default) | Shift_Configuration |
| HC_Summary | List (default) | Headcount_Calculator |
| HC_Gap_Alert_Log | List (filtered) | Headcount_Calculator |
| Shift_Utilisation_Summary | List (grouped) | Headcount_Calculator |
| All_HC_Actual | List (default) | HC_Actual_Entry |
| Department_HC_Actual | List (grouped) | HC_Actual_Entry |
| All_Parts | List (default) | Part_SKU_Master |
| Active_Parts | List (filtered) | Part_SKU_Master |
| ADU_History | List | Part_SKU_Master |
| All_Decoupling_Points | List (default) | Decoupling_Point_Master |
| Active_Decoupling_Points | List (filtered) | Decoupling_Point_Master |
| All_Buffer_Profiles | List (default) | Buffer_Profile_Levels |
| All_Stock_Snapshots | List (default) | Daily_Stock_Snapshot |
| Latest_Stock_Snapshots | List (sorted) | Daily_Stock_Snapshot |
| All_NFP_Status | List (default, RAG coloring) | NFP_Status_Log |
| Parts_In_RED | List (filtered) | NFP_Status_Log |
| NFP_Trend | List (14-day trend) | NFP_Status_Log |
| All_Supply_Alerts | List (default, with Acknowledge button) | Supply_Alert_Log |
| Unacknowledged_Alerts | List (filtered, with Acknowledge button) | Supply_Alert_Log |
| Alert_ADU_Ref | List | Supply_Alert_Log |

## Pages

| Page Name | Purpose | Key Components |
|---|---|---|
| Headcount_Dashboard | HC module overview | KPI cards (required/gap/utilisation), dept chart, shift summary, alert panel, weekly trend |
| DDMRP_Buffer_Dashboard | DDMRP module overview | Buffer KPI cards (RED/YELLOW/GREEN counts, unack alerts), RAG table, RED parts panel, supply alerts panel, NFP trend |

## Design Decisions

- **HC Formula**: `Required_HC = (Planned_Output × Cycle_Time_Seconds) / (Available_Hours × 3600 × Efficiency% / 100)` — calculated on-success workflow, writes back to same record.
- **DDMRP Buffer Formula**: Red = MOQ + (ADU × LT × LTF); Yellow = ADU × LT; Green = max(MOQ, ADU × OC, Red) — computed by daily schedule at 06:00 IST.
- **NFP = On_Hand_Qty + On_Order_Qty − Qualified_Demand** — calculated from Daily_Stock_Snapshot.
- **ADU is manual input** on Part_SKU_Master (no Consumption History form).
- **Integrations deferred**: Zoho Cliq alerts and Zoho Books PO creation have TODO comments in workflows; require connection configuration before activation.
- **ADU_History report** is a Supply_Alert_Log report (shows alert history for ADU tracking); separate `ADU_History` based on Part_SKU_Master is accessed via the Part Master section.
- **6 profiles**: HR_Admin, Line_Manager, Production_Planner, Supply_Planner, Procurement, Operations_Head — each with scoped CRUD permissions.
- **Web-only UI**: No phone/tablet menus or layouts (per project decision).
