## Application Overview
Vendor Scorecard manages vendor setup, qualification, onboarding, and performance review in a segregated Creator app structure. Configuration masters drive scoring, master forms hold vendor reference data, transaction forms manage lifecycle activity, and a native dashboard summarizes operational health.

## Forms
| Form Name | Purpose | Key Lookups |
|---|---|---|
| Categories | Shared configuration categories | None |
| Criteria | Scoring criteria by process | Category -> Categories |
| Weightages | Effective-dated criteria weights | Criteria -> Criteria |
| Rating_Scales | Result bands and acceptability | None |
| App_Users | Internal user master | Department -> Categories |
| Vendors | Vendor master and lifecycle summary | Config category/product category -> Categories |
| Vendor_Contacts | Vendor contact master | Vendor -> Vendors |
| Products_Services | Vendor offerings | Vendor -> Vendors, Category -> Categories |
| Vendor_Documents | Vendor document tracking | Vendor -> Vendors, Document_Type -> Categories |
| Vendor_Registration | Vendor registration transaction | Linked_Vendor -> Vendors |
| Vendor_Evaluations | Evaluation scoring | Vendor -> Vendors, Category -> Categories |
| Risk_Assessments | Risk scoring and mitigation | Vendor -> Vendors, Category -> Categories |
| Vendor_Onboarding | Onboarding checklist and activation | Vendor -> Vendors, Category -> Categories |
| Vendor_Performance_Metrics | Monthly performance review | Vendor -> Vendors |

## Reports
| Report Name | Type | Source Form |
|---|---|---|
| Configuration lists | List | Categories, Criteria, Weightages, Rating_Scales |
| Master lists | List | App_Users, Vendors, Contacts, Products/Services, Documents |
| Vendor_Lifecycle_Board | Kanban | Vendors |
| Registration reports | List | Vendor_Registration |
| Evaluation reports | List | Vendor_Evaluations |
| Risk reports | List | Risk_Assessments |
| Onboarding reports | List | Vendor_Onboarding |
| Performance reports | List | Vendor_Performance_Metrics |

## Pages
| Page Name | Purpose | Key Components |
|---|---|---|
| Vendor_Scorecard_Dashboard | Native management dashboard for lifecycle, risk, registration, document, onboarding, and performance health | KPI panels, native charts, gauge, report embeds, lifecycle board launch panel |

## Design Decisions
- Menu segregation follows Configuration, Masters, Transactions, Reports, and Dashboard concepts.
- Configurable scoring uses Criteria, Weightages, and Rating Scales, with safe fallback formulas.
- Lifecycle stages remain Registered, Evaluated, Risk Assessed, Onboarded, Active, Performance Reviewed.
- No widgets are used; dashboard uses Creator-native components and supported panels.