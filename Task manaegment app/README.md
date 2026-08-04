## Application Overview
A small-team task management app for organizing projects, assigning tasks, and tracking work through simple statuses. Managers can oversee projects and workload, while team members can update tasks and add comments with follow-up dates.

## Forms
| Form Name | Purpose | Key Lookups |
|---|---|---|
| Projects | Stores project details, manager, planned dates, priority, and status. | Project Manager -> Creator users |
| Tasks | Tracks work items, assignees, due dates, priorities, status, and hours. | Project -> Projects; Assigned To -> Creator users |
| Comments | Captures task updates, blockers, questions, and follow-up notes. | Task -> Tasks |

## Reports
| Report Name | Type | Source Form |
|---|---|---|
| All_Projects | List | Projects |
| Active_Projects | List | Projects |
| Project_Calendar | Calendar | Projects |
| All_Tasks | List | Tasks |
| My_Open_Tasks | List | Tasks |
| Task_Board | Kanban | Tasks |
| Overdue_Tasks | List | Tasks |
| Task_Calendar | Calendar | Tasks |
| All_Comments | List | Comments |
| Follow_Up_Comments | List | Comments |

## Pages
| Page Name | Purpose | Key Components |
|---|---|---|
| Task_Dashboard | Summarizes project and task health. | KPI cards, status breakdown, priority/workload view, recent activity, embedded overdue tasks, embedded task board |

## Design Decisions
- Uses Creator system users for project managers and task assignees instead of duplicating a user directory.
- Keeps task workflow simple with editable statuses rather than a formal approval blueprint.
- Uses dynamic on-load and on-user-input workflows for completion and blocker fields.
- Adds mandatory web quick/detail layouts for every report.
