# FFSC Training & Delivery System

## Application Overview
A comprehensive multi-centre skill training management system replacing manual Excel workflows. It provides a single source of truth spanning centre operations, batch execution, learner lifecycle, finance tracking, and CEO-level exception management across a network of skill academies.

## Forms

| Form Name | Purpose | Key Lookups |
|---|---|---|
| Centre_Master | Static profile + live summary for each academy centre | — |
| Batch_Operations | Tracks every training batch with funding, lifecycle, and risk | → Centre_Master |
| Program_Utilization | Monthly capacity planning snapshot per centre | → Centre_Master |
| Academy_PL | Monthly P&L with full revenue & cost breakdown | → Centre_Master |
| Batch_Wise_Expense | Granular batch-level expense tracking (reconciled from field data) | → Batch_Operations |
| IPG_Funding_Support | IP&G / partner funding lifecycle tracking | → Centre_Master, Batch_Operations |
| TD_Revenue_Pipeline | Standalone opportunity pipeline for T&D revenue | → Centre_Master (optional) |
| Learner_Lifecycle_DB | One record per learner covering mobilisation → alumni | → Centre_Master, Batch_Operations |
| Trainer_Daily_Report | Daily attendance, topic, and completion log per batch | → Batch_Operations |
| Academy_Monthly_Update | Monthly status rollup submitted by TM/Trainer | → Centre_Master |
| CEO_Action_Box | Standalone task/decision tracker for CEO Office | → Centre_Master, Batch_Operations (optional) |

## Reports

| Report Name | Type | Source Form |
|---|---|---|
| All_Centres | List (default) | Centre_Master |
| Centres_By_Status | List (grouped) | Centre_Master |
| Active_Centres | List (filtered) | Centre_Master |
| All_Batches | List (default) | Batch_Operations |
| Active_Batches | List (filtered) | Batch_Operations |
| Batches_By_Centre | List (grouped) | Batch_Operations |
| CEO_Action_Batches | List (filtered) | Batch_Operations |
| All_Program_Utilization | List (default) | Program_Utilization |
| Program_Utilization_By_Centre | List (grouped) | Program_Utilization |
| All_Academy_PL | List (default) | Academy_PL |
| Academy_PL_By_Centre | List (grouped) | Academy_PL |
| Pending_Validation | List (filtered) | Academy_PL |
| All_Batch_Expenses | List (default) | Batch_Wise_Expense |
| Expenses_By_Batch | List (grouped) | Batch_Wise_Expense |
| All_IPG_Funding | List (default) | IPG_Funding_Support |
| Pending_Funding | List (filtered) | IPG_Funding_Support |
| Funding_By_Centre | List (grouped) | IPG_Funding_Support |
| All_Revenue_Pipeline | List (default) | TD_Revenue_Pipeline |
| Pipeline_By_Stage | List (grouped) | TD_Revenue_Pipeline |
| CEO_Help_Pipeline | List (filtered) | TD_Revenue_Pipeline |
| All_Learners | List (default) | Learner_Lifecycle_DB |
| Learners_By_Stage | List (grouped) | Learner_Lifecycle_DB |
| Learners_By_Batch | List (grouped) | Learner_Lifecycle_DB |
| Placed_Learners | List (filtered) | Learner_Lifecycle_DB |
| Lifecycle_Funnel | List (pivot-style grouped) | Learner_Lifecycle_DB |
| All_Trainer_Reports | List (default) | Trainer_Daily_Report |
| Recovery_Needed | List (filtered) | Trainer_Daily_Report |
| Reports_By_Batch | List (grouped) | Trainer_Daily_Report |
| All_Monthly_Updates | List (default) | Academy_Monthly_Update |
| CEO_Escalations | List (filtered) | Academy_Monthly_Update |
| Updates_By_Centre | List (grouped) | Academy_Monthly_Update |
| All_CEO_Actions | List (default) | CEO_Action_Box |
| Open_CEO_Actions | List (filtered) | CEO_Action_Box |
| CEO_Actions_By_Status | List (grouped) | CEO_Action_Box |

## Pages

| Page Name | Purpose | Key Components |
|---|---|---|
| CEO_Dashboard | Executive KPI dashboard | KPI_Cards.dshtml, Financial_Summary.dshtml, RAG_Status.dshtml, Open_Actions (embedded report) |

## Design Decisions

- **RAG is manually set** — no threshold-based auto-computation; kept simple per user decision.
- **Aadhaar field** hidden at profile level for Trainer and IPG_Team; visible to TM, T&D Office, Finance, CEO Office.
- **Funding gate** enforced via on-validate workflow: Start_Date blocked if Funding_Confirmed ≠ "Yes".
- **RAG escalation** on Batch Risk_Flag change: Red → notifies TM + Trainer; Amber → notifies T&D Office.
- **Formula rollups** (Current_Candidate_Count, Candidates_Trained, etc.) use Creator's aggregate expression engine, not manual entry.
- **Batch_Wise_Expense** included as a separate form (reconciled from Center_Wise_Details Excel sheet) to feed into Academy P&L cost heads.
- **Lifecycle_Funnel** built as a grouped list report rather than a separate form — counts learners by stage per batch.
- **All currency fields** use INR with Indian comma format (commadotindian).
- **CEO Dashboard** uses HTML snippets (dshtml) for KPI cards and RAG badges, with an embedded Open_CEO_Actions report.
