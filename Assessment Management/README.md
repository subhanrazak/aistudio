## Application Overview
Kannanware Current State Assessment Solution manages consultant-led and Customer Portal assessments from setup through response capture, scoring, report tracking, reminders, and reassessment. It uses industry questionnaires, response snapshots, internal-only report document handling, and dashboard pages for tracking.

## Forms
| Form Name | Purpose | Key Lookups |
|---|---|---|
| Industry_Types | Industry master | — |
| Customers | Customer profile/assignment | Industry_Types |
| Projects | Customer project tracking | Customers, Industry_Types |
| Project_Documents | File/link tracking | Projects, Customers, Assessments |
| Master_Questionnaire | Industry question bank | Industry_Types |
| Question_Option_Scores | Selectable-answer scoring | Master_Questionnaire, Industry_Types |
| Scoring_Maturity_Config | Maturity/risk ranges | Industry_Types |
| Assessment_Settings | Validity/reminder defaults | — |
| Assessments | Assessment lifecycle | Customers, Projects, Industry_Types |
| Assessment_Responses | Snapshot responses | Assessments, Customers, Projects, Master_Questionnaire |
| Report_Email_Log | Email audit trail | Assessments, Projects, Customers, Project_Documents |
| Activity_Log | Activity feed | Customers, Projects, Assessments |

## Reports
| Report Name | Type | Source Form |
|---|---|---|
| Industry type reports | List | Industry_Types |
| Customer reports | List | Customers |
| Project reports/board | List/Kanban | Projects |
| Document reports | List | Project_Documents |
| Questionnaire reports | List | Master_Questionnaire |
| Option score reports | List | Question_Option_Scores |
| Maturity config reports | List | Scoring_Maturity_Config |
| Assessment setting reports | List | Assessment_Settings |
| Assessment lists/board | List/Kanban | Assessments |
| Response reports | List | Assessment_Responses |
| Email log reports | List | Report_Email_Log |
| Activity reports | List | Activity_Log |

## Pages
| Page Name | Purpose | Key Components |
|---|---|---|
| Current_State_Dashboard | Operations overview | KPI cards, summaries, expiry queues, activity feed |
| Project_Tracking_Dashboard | Project-level tracking | Summary, latest assessment, documents, activity links |

## Design Decisions
- Portal users cannot access generated report files/links or internal dashboards.
- Reassessment reuses the same assessment record; old reports stay in Project_Documents.
- Assessment_Responses stores question snapshots for questionnaire-version history.
- Report buttons generate responses, submit/score, reopen reassessment, and log emails.
- Daily schedule sends 4-day reminders until expiry and marks expired assessments.