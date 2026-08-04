## Application Overview
Family Health Tracker is a Zoho Creator customer-portal app for caregivers to manage household health information in one authenticated workspace. It tracks family profiles, health records, prescriptions, medications, fixed-time reminders, OCR scan review, and reminder audit logs.

## Forms
| Form Name | Purpose | Key Lookups |
|---|---|---|
| Family_Members | Household member health profiles | None |
| Health_Records | Consultations, labs, prescriptions, vaccinations | Member → Family_Members |
| Medications | Medication courses and reminder slots | Member → Family_Members |
| Reminder_Log | Sent/failed reminder audit trail | Medication → Medications; Member → Family_Members |
| Prescription_Scans | Upload prescriptions and review Zia OCR text | Member → Family_Members; Saved_Health_Record → Health_Records |

## Reports
| Report Name | Type | Source Form |
|---|---|---|
| All_Family_Members | List | Family_Members |
| Family_Member_Directory | List | Family_Members |
| All_Health_Records | List | Health_Records |
| Health_Record_Timeline | Timeline | Health_Records |
| Vaccination_Records | List | Health_Records |
| All_Medications | List | Medications |
| Active_Medications | List | Medications |
| Medication_Course_Calendar | Calendar | Medications |
| Todays_Reminder_Log | List | Reminder_Log |
| All_Reminder_Log | List | Reminder_Log |
| All_Prescription_Scans | List | Prescription_Scans |
| Pending_Prescription_Review | List | Prescription_Scans |

## Pages
| Page Name | Purpose | Key Components |
|---|---|---|
| Health_Dashboard | Landing dashboard | KPI cards, quick actions, recent activity, upcoming reminders |
| Todays_Reminders | Read-only daily medication plan | Summary counters, grouped reminder cards, reminder log table |

## Design Decisions
- Customer portal profile `Caregiver_Portal` gates all app access.
- `Owner_Email` plus validation workflows keep records tied to the logged-in caregiver.
- Fixed reminder slots use daily schedules and `Reminder_Log` for duplicate prevention.
- Prescription scanning uses Zia OCR and stores both extracted and reviewed text.
- Dashboard pages use responsive HTML snippets for richer web UI control.
