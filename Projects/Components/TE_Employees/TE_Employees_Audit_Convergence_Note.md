# TE_Employees audit convergence note

`TE_Audit_Log` was not present when `TE_Employees` was generated, so `FormWorkflows/TE_Employees_On_Success.ds` intentionally avoids a direct `TE_Audit_Log` insert to prevent compile-time form-link errors.

When the audit form exists, replace the placeholder `info` action with an audit insert that records:

- entity type: `Employee`
- action: `create/update` (or split add/edit workflows to capture exact create vs update)
- actor: `zoho.loginuser`
- timestamp: `zoho.currenttime`
- key employee ID: `input.Employee_ID`
