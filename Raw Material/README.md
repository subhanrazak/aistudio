# Raw Material Shelf-Life Monitor

## Application Overview
A Zoho Creator surround app for SAP MM/QM Batch Management (app link: `rm_shelf_life_monitor`). It monitors raw material batch expiry dates with a traffic-light dashboard (Red/Amber/Green), drives a multi-stage disposition approval Blueprint, logs FEFO compliance, and provides rich analytics dashboards. SAP integration is stubbed — data is entered manually; field schema mirrors SAP tables (MCH1, MCHB, MARA, T001L) for future ODBC connectivity.

---

## Forms

| Form Name | Purpose | Key Lookups |
|---|---|---|
| Material_Groups | Configurable alert thresholds (Amber/Red days) per material group | — |
| Storage_Locations | Warehouse locations (mirrors SAP T001L LGORT/LGOBE) | — |
| Materials | Material master (MARA/MAKT); stores standard cost for Value at Risk | Material_Groups |
| Batch_Monitor | Core form — one record per SAP batch; computes status & VAR | Materials, Storage_Locations |
| Disposition_Actions | Tracks disposition requests with 5-stage Blueprint approval | Batch_Monitor |
| FEFO_Log | Manual goods-issue log for FEFO compliance tracking | Materials, Batch_Monitor |

---

## Reports

| Report Name | Type | Source Form |
|---|---|---|
| All_Material_Groups | List | Material_Groups |
| All_Storage_Locations | List | Storage_Locations |
| All_Materials | List | Materials |
| Materials_By_Group | List (grouped) | Materials |
| All_Batches | List (default, conditional formatting) | Batch_Monitor |
| Red_Alert_Batches | List (filtered) | Batch_Monitor |
| Amber_Warning_Batches | List (filtered) | Batch_Monitor |
| Status_Kanban | Kanban | Batch_Monitor |
| Expiry_Calendar | Calendar | Batch_Monitor |
| Top_5_Urgent_Batches | List | Batch_Monitor |
| All_Dispositions | List (conditional formatting) | Disposition_Actions |
| Pending_Dispositions | List (filtered) | Disposition_Actions |
| Disposition_Kanban | Kanban | Disposition_Actions |
| All_FEFO_Logs | List (conditional formatting) | FEFO_Log |
| GI_Calendar | Calendar | FEFO_Log |

---

## Pages

| Page Name | Purpose | Key Components |
|---|---|---|
| Shelf_Life_Dashboard | Main analytics hub | Traffic-light KPI cards, Value at Risk, Expiry Timeline chart, FEFO gauge, Top 10 Materials (HTML snippet), VAR by group (HTML snippet), Disposition tracker, Monthly trend chart, Top 5 urgent batches |

---

## Design Decisions

- **Status_Color stored picklist** (not formula): Status must persist between page loads and be sortable/filterable in reports; formula would recompute on every view but can't be reliably filtered.
- **Std_Cost_Per_Unit copied on save**: Avoids unreliable lookup dot notation in formula fields (`Material.Standard_Cost`); an on-success workflow copies it from the Materials record.
- **Material_Group_Name denormalized on batch**: Allows HTML snippet VAR-by-group and Top-10-materials snippets to aggregate efficiently without cross-form aggregation.
- **Blueprint for Disposition Workflow**: 5-stage Blueprint (Pending → In Review → Pending Re-test → Approved/Rejected) with action-type-based transition owner rules: Consume=Warehouse Manager; Return to Vendor=Admin; Extend=QA Manager (re-test path); Dispose/Transfer=QA+Controller.
- **Nightly schedule uses range() pagination**: Deluge has no `while` loop; schedule processes 3 blocks of 200 records (up to 600 batches) per run using `range from X to Y`.
- **Boards replaced by dshtml snippets**: Creator compiler disallows `<board>` inside `<pc>` elements; Top-10 and VAR-by-group components are implemented as pure HTML snippets.
- **Four profiles**: Warehouse_Manager, QA_Manager, Plant_Controller, Admin — covers all BRD approver roles with the minimum viable profile set.
