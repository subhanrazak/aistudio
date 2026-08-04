## Application Overview
Small-clinic app for patients, appointments, consultations, prescriptions, insurance billing, claims, payments, and audit history. It uses simple Staff access with stronger privacy controls for health, personal, financial, and audit-sensitive data.

## Forms
| Form Name | Purpose | Key Lookups |
|---|---|---|
| Insurance_Providers | Insurer directory | None |
| Staff_Members | Staff/doctor directory | None |
| Patients | Patient profile and insurance | Insurance_Providers |
| Appointments | Visit scheduling/status | Patients, Staff_Members |
| Consultations | Clinical notes and follow-ups | Patients, Appointments, Staff_Members |
| Prescriptions | Medication/refill tracking | Patients, Consultations, Staff_Members |
| Invoices | Charges and balances | Patients, Appointments, Consultations |
| Insurance_Claims | Claim lifecycle | Patients, Insurance_Providers, Invoices |
| Payments | Receipts and invoice updates | Invoices |
| Audit_Logs | Restricted system history | None |

## Reports
| Report Name | Type | Source Form |
|---|---|---|
| All_Insurance_Providers, Active_Insurance_Providers | List | Insurance_Providers |
| Staff_Directory, Active_Doctors | List | Staff_Members |
| All_Patients, Active_Patients, Patient_Insurance_Status | List | Patients |
| All_Appointments, Today_Appointments | List | Appointments |
| Appointment_Calendar | Calendar | Appointments |
| Appointment_Status_Board | Kanban | Appointments |
| All_Consultations, Recent_Consultations | List | Consultations |
| Follow_Up_Calendar | Calendar | Consultations |
| All_Prescriptions, Active_Prescriptions, Patient_Prescription_History | List | Prescriptions |
| All_Invoices, Outstanding_Invoices, Paid_Invoices | List | Invoices |
| All_Insurance_Claims, Open_Insurance_Claims | List | Insurance_Claims |
| Claim_Status_Board | Kanban | Insurance_Claims |
| All_Payments, Received_Payments, Payment_Register | List | Payments |
| All_Audit_Logs, High_Sensitivity_Audits | List | Audit_Logs |

## Pages
| Page Name | Purpose | Key Components |
|---|---|---|
| Clinic_Dashboard | Web operations dashboard | KPIs, summaries, activity feed, open work tables |

## Design Decisions
- PII/ePHI fields are marked and key clinical values encrypted.
- Dynamic fields use on-load/on-input workflows.
- Audit logs are workflow-populated and hidden from Staff.
- Claim approval/denial is Administrator-only via blueprint.
- Invoice totals use formulas; payments update invoices.
