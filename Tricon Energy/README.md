## Application Overview
Tricon Energy is a Zoho Creator pricing and quote management app for customer-specific polymer/resin pricing. It centralizes master data, commercial terms, supplier prices, logistics costs, FX rates, pricing requests, calculated options, generated quote records, dashboards, and audit history.

## Forms
| Form Name | Purpose | Key Lookups |
|---|---|---|
| Customers | Customer master and quote defaults | - |
| Customer_Branches | Delivery locations and branch defaults | Customers, Arrival_Ports, Packaging_Options |
| Product_Catalog | Product master and default vendor/currency/duty | Vendors |
| Vendors | Supplier/vendor master | - |
| Arrival_Ports | Port master for landed cost logic | - |
| Packaging_Options | Packaging master and quantity defaults | - |
| Delivery_Models | Delivery/incoterm model master | - |
| Customer_Tier_Rules | Tier thresholds by application/resin | - |
| Customer_Product_Profiles | Customer-product tier assignment | Customers, Product_Catalog, Customer_Tier_Rules |
| Customer_Commercial_Agreements | Customer pricing terms and defaults | Customers, Customer_Branches, Packaging_Options, Delivery_Models |
| FX_Rates | Approved exchange-rate history | - |
| Supplier_Price_Books | Supplier CIF prices by product/vendor | Product_Catalog, Vendors, Arrival_Ports, Packaging_Options |
| Logistics_Cost_Matrix | Landed logistics cost matrix | Arrival_Ports, Packaging_Options, Delivery_Models |
| Pricing_Requests | Parent pricing request and approval status | Customers, Customer_Branches |
| Pricing_Options | Calculated quote scenarios under requests | Pricing_Requests, Customers, Product_Catalog, Vendors, cost masters |
| Quote_Documents | PDF-ready quote snapshots | Pricing_Requests, Customers |
| Audit_Logs | Audit trail for critical activity | Customers, Pricing_Requests |

## Reports
| Report Name | Type | Source Form |
|---|---|---|
| Master data reports | List | Customers, branches, products, vendors, ports, packaging, delivery models |
| Rule and cost reports | List | tier rules, product profiles, agreements, FX, supplier prices, logistics matrix |
| Pricing pipeline reports | List/Kanban | Pricing_Requests |
| Pricing option reports | List | Pricing_Options |
| Quote reports | List | Quote_Documents |
| Audit reports | List | Audit_Logs |

## Pages
| Page Name | Purpose | Key Components |
|---|---|---|
| Pricing_Dashboard | Management pricing workspace | KPI cards, pipeline summary, missing-input table, approval queue, audit feed |

## Design Decisions
- Calculation fields are stored as snapshots so quotes do not change when live costs or FX rates are updated.
- Sales users can create pricing work but sensitive cost inputs/results are hidden or read-only.
- Audit logging is centralized and append-only in permissions.
- Every report has a mandatory web quick/detail DeviceUI layout and is reachable from the web menu.
