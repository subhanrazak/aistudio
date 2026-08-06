## Application Overview
Vendor Scorecard Tracker manages vendor masters, products/services, internal users, company structure, registration, onboarding, evaluation, risk, and performance reviews. The web menu is arranged into Master Data, Configuration Data, Transaction Reports, dashboards, and shared analytics for cleaner navigation.

## Forms
| Form Name | Purpose | Key Lookups |
|---|---|---|
| Vendors | Vendor master and score summary | - |
| Contacts | Vendor contact persons | Vendors |
| Products_Services | Vendor offerings | Vendors |
| Documents | Vendor document tracking | Vendors |
| Users | Internal app users/evaluators | - |
| Company_Details | Company/legal entity master | - |
| Branches | Branch/location master | Company_Details, Users |
| Departments | Department/cost center master | Company_Details, Branches, Users |
| Categories | Evaluation/risk/performance categories | - |
| Criteria | Scoring criteria | Categories |
| Weightages | Process/category/criteria weights | Categories, Criteria |
| Rating_Scales | Rating-to-score setup | - |
| Workflow_Configuration | Workflow status and SLA setup | - |
| Registration | Vendor registration tracking | Vendors |
| Evaluation | Vendor evaluation score rows | Vendors, Users, Criteria, Rating_Scales |
| Risk_Assessment | Vendor risk score rows | Vendors, Users, Criteria, Rating_Scales |
| Onboarding | Vendor onboarding tracker | Vendors, Users |
| Performance_Review | Periodic review score rows | Vendors, Users, Criteria, Rating_Scales |

## Reports
| Report Name | Type | Source Form |
|---|---|---|
| All_Vendors / Vendor_Pipeline | List, Kanban | Vendors |
| All_Contacts / Primary_Contacts | List | Contacts |
| Vendor_Products_Services / Critical_Products_Services | List | Products_Services |
| Vendor_Documents / Expiring_Documents | List | Documents |
| All_Users / Evaluators | List | Users |
| All_Company_Details / Active_Company_Details | List | Company_Details |
| All_Branches / Active_Branches / Branches_By_Company | List | Branches |
| All_Departments / Active_Departments / Departments_By_Branch | List | Departments |
| All_Categories / Active_Categories | List | Categories |
| All_Criteria / Criteria_By_Category | List | Criteria |
| Active_Weightages / Weightages_By_Process | List | Weightages |
| All_Rating_Scales / Rating_Scales_By_Process | List | Rating_Scales |
| Workflow_Statuses | List | Workflow_Configuration |
| Vendor_Registrations / Registration_Status_Board | List, Kanban | Registration |
| Vendor_Evaluations / Evaluation_Scores | List | Evaluation |
| Risk_Assessments / High_Risk_Assessments | List | Risk_Assessment |
| Onboarding_Tracker / Onboarding_By_Status | List, Kanban | Onboarding |
| Performance_Reviews / Performance_Scores | List | Performance_Review |

## Pages
| Page Name | Purpose | Key Components |
|---|---|---|
| Vendor_Overview_Dashboard | Executive vendor overview | KPI panels, charts, gauge, report embeds, scorecards |
| Vendor_Scorecard_Dashboard | Vendor-specific scorecard | Vendor KPIs, gauges, category charts, filtered reports |

## Design Decisions
- Web navigation is grouped as Master Data and Configuration Data per the latest request.
- Company Structure uses separate Company, Branch, and Department master forms.
- New company structure modules are internal-only; portal profiles were not granted access.
- Forms remain hidden in menus; reports and dashboards are the primary navigation entries.
- Theme is set with `new theme = 104`; widgets are avoided.