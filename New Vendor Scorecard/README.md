## Application Overview
Vendor Scorecard manages vendor configuration, masters, registrations, onboarding, risk, evaluation, and performance reviews. It provides weighted scoring, status-only automation, role-based access, mobile-friendly dashboards, and vendor-wise scorecards.

## Forms
| Form Name | Purpose | Key Lookups |
|---|---|---|
| Categories | Scorecard category setup | - |
| Criteria | Scoring criteria | Categories |
| Weightages | Process weights | Categories, Criteria |
| Rating_Scales | Rating-to-score setup | - |
| Workflow_Configuration | Status/SLA setup | - |
| Users | Business user master | - |
| Vendors | Vendor master/score summary | - |
| Contacts | Vendor contacts | Vendors |
| Products_Services | Vendor offerings | Vendors |
| Documents | Document tracking | Vendors |
| Registration | Vendor registration | Vendors |
| Evaluation | Evaluation score rows | Vendors, Users, Criteria, Rating_Scales |
| Risk_Assessment | Risk score rows | Vendors, Users, Criteria, Rating_Scales |
| Onboarding | Onboarding tracker | Vendors, Users |
| Performance_Review | Periodic review rows | Vendors, Users, Criteria, Rating_Scales |

## Reports
| Report Name | Type | Source Form |
|---|---|---|
| All_Categories / Active_Categories | List | Categories |
| All_Criteria / Criteria_By_Category | List | Criteria |
| Active_Weightages / Weightages_By_Process | List | Weightages |
| All_Rating_Scales / Rating_Scales_By_Process | List | Rating_Scales |
| Workflow_Statuses | List | Workflow_Configuration |
| All_Users / Evaluators | List | Users |
| All_Vendors / Vendor_Pipeline | List, Kanban | Vendors |
| All_Contacts / Primary_Contacts | List | Contacts |
| Vendor_Products_Services / Critical_Products_Services | List | Products_Services |
| Vendor_Documents / Expiring_Documents | List | Documents |
| Vendor_Registrations / Registration_Status_Board | List, Kanban | Registration |
| Vendor_Evaluations / Evaluation_Scores | List | Evaluation |
| Risk_Assessments / High_Risk_Assessments | List | Risk_Assessment |
| Onboarding_Tracker / Onboarding_By_Status | List, Kanban | Onboarding |
| Performance_Reviews / Performance_Scores | List | Performance_Review |

## Pages
| Page Name | Purpose | Key Components |
|---|---|---|
| Vendor_Overview_Dashboard | Executive dashboard | KPI panels, charts, gauge, report embeds, HTML scorecards |
| Vendor_Scorecard_Dashboard | Vendor-specific dashboard | KPIs, gauges, category charts, filtered reports |

## Design Decisions
- Forms are hidden; menus expose dashboards and key reports.
- Profiles cover admin, procurement, evaluator, registering vendor, and onboarded vendor users.
- Weighted scores are calculated by workflow; no blueprints are used.
- Theme/new theme is 104; widgets are avoided.
- Vendor scorecards use the `Vendor_ID` page parameter.