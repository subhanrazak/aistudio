# TE_Sync_Log implementation notes

- Phase 1 SAP polling is represented by `TE_Sync_Log_SAP_Polling_Schedule.ds`; it creates placeholder log rows only.
- No Connection, DataSource, ODBC credential, or live connector file is defined for this component.
- The available schedule DS supports daily/weekly/monthly/yearly frequency only, so the requested every-2-hours business-day cadence is represented as a daily placeholder schedule with each row's `Next_Scheduled_Run` set two hours later.