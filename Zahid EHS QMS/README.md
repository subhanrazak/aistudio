## Application Overview
This HR recruitment application helps the HR team manage openings, applicants, interviews, offers, and hired employees in one workflow. It supports HR recruiters, hiring managers, and interviewers with separate access levels and a dashboard for pipeline visibility.

## Forms
| Form Name | Purpose | Key Lookups |
|---|---|---|
| Departments | Department master for openings and employees | None |
| Job_Openings | Vacancy and role tracking | Departments |
| Applicants | Candidate profile, contact, resume, skills | None |
| Applications | Applicant-to-opening pipeline with selection stages | Applicants, Job_Openings |
| Interviews | Interview scheduling and feedback | Applications |
| Offers | Offer tracking and hire conversion | Applications, Departments |
| Employees | Basic employee records for accepted candidates | Departments, Applications |

## Reports
| Report Name | Type | Source Form |
|---|---|---|
| All_Departments / Active_Departments | List | Departments |
| All_Job_Openings / Open_Job_Openings | List | Job_Openings |
| Openings_By_Status | Kanban | Job_Openings |
| All_Applicants / Active_Applicants | List | Applicants |
| All_Applications / Applications_For_Offer / Rejected_Withdrawn_Applications | List | Applications |
| Application_Pipeline | Kanban | Applications |
| All_Interviews / Pending_Feedback | List | Interviews |
| Interview_Calendar | Calendar | Interviews |
| All_Offers / Accepted_Offers | List | Offers |
| Offer_Status_Board | Kanban | Offers |
| All_Employees / Active_Employees | List | Employees |

## Pages
| Page Name | Purpose | Key Components |
|---|---|---|
| Recruitment_Dashboard | Recruitment overview for HR and managers | KPI cards, pipeline summary, interview table, openings, offers, hires |

## Design Decisions
- Applicant-to-opening progress is stage controlled through an Applications blueprint.
- Accepted offers create one employee record per source application.
- Dynamic form workflows show decision or feedback fields only when relevant.
- PII fields are marked on applicant/employee contact data for profile-level control.
- Web UI includes every report with mandatory quick/detail layouts.