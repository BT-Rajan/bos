# 07 - Calendar & Escalation Engine

The single most important shared component in the system. Everything in `02-Functional-Scope.md` that has a due date routes through this.

## State Machine (shared by tasks, submissions, milestones)

```
Not Started → In Progress → Due Today → Overdue → Escalated
                                  ↓            ↓
                              Completed    Completed (late)
```

- **Due Today**: the sweep job marks any item whose due date is today (business timezone) and not yet completed.
- **Overdue**: the sweep job marks any item whose due date has passed and not yet completed.
- **Escalated**: set explicitly by a person via the escalate action — never automatic. Automatic escalation would remove the human judgment call the design deliberately preserves.
- An overdue item requires one of: complete (late), follow-up (note logged, stays open), reschedule (new due date, original preserved), or escalate (notifies the assignee's manager).

## Timezone Rule

All due-date comparisons ("is this today," "has this passed") evaluate against the business timezone configured in `backend/app/core/config.py` (Asia/Kuwait, no DST) — never server-local time, never naive UTC. This is decided once, referenced everywhere.

## The Sweep Job

Runs on a schedule (e.g., hourly, with the authoritative check at business-day boundary):
1. Query all Task/GovernmentSubmission/ContractMilestone rows where due-date ≤ today (business tz) and status not in (Completed, Escalated).
2. Flip status to Due Today or Overdue as appropriate.
3. For newly-Overdue items, create nothing automatically beyond the status flip — escalation itself stays a human action, per the state machine above.
4. Fire a notification to the assignee (and, after a configurable grace period, their manager) for anything still Overdue.

## Calendar Aggregation Query (conceptual)

```sql
SELECT 'task' AS entity_type, id, project_id, tentative_completion_date AS due_date, status FROM tasks
UNION ALL
SELECT 'government_submission', id, project_id, deadline, status FROM government_submissions
UNION ALL
SELECT 'contract_milestone', id, project_id, milestone_date, status FROM contract_milestones
WHERE due_date BETWEEN :from AND :to
  AND (assignee_id = :user OR :user IS NULL)  -- team rollup omits this filter
```

Escalation records are joined in by `(entity_type, entity_id)`, not stored redundantly per source table.

## Escalation Table

One polymorphic table, `escalations`: `entity_type`, `entity_id`, `status`, `note`, `rescheduled_to_date`, `created_by`, `created_at`. Government submissions and contract milestones reuse this unchanged — no new table, no new logic, when those domains are built.

## Manager Rollup

`GET /calendar/team` reuses the same aggregation query with the user filter replaced by "all users reporting to me" (via `User.manager_id`), so the rollup view is a parameterization of the same engine, not a separate implementation.
