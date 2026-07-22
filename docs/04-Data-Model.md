# 04 - Unified Data Model

Core entities and the relationships that matter for the Calendar/Escalation engine. Field lists are representative, not exhaustive — exact columns are finalized during the matching build pass.

## Identity & Org
- **User** — id, name, email, role_id, manager_id (nullable, for rollup routing)
- **Role** / **Permission** — RBAC
- **Company** — single row, org-wide settings

## Client & Project
- **Client** — id, name, contacts[]
- **Project** — id, client_id, name, status, owner_id

## The Three Calendar Sources (share one shape at the aggregation boundary)
- **Task** — id, project_id, assignee_id, title, **tentative_completion_date** (required), status
- **GovernmentSubmission** — id, project_id, authority_id, form_id, **deadline** (required), status
- **ContractMilestone** — id, contract_id, project_id, **milestone_date** (required), status

Each of the three has: id, owning project_id, a due-date column, and a status value drawn from the shared enum (`not_started / in_progress / due_today / overdue / escalated / completed`). This shared shape is what lets `04-Data-Model.md`'s calendar query stay a single `UNION` rather than three bespoke queries — see `07-Calendar-Escalation-Engine.md`.

## Escalation (generic, polymorphic — built once)
- **Escalation** — id, entity_type (`task` / `government_submission` / `contract_milestone`), entity_id, status, note, rescheduled_to_date (nullable), created_by, created_at

## Supporting Entities
- **Document** — id, project_id, uploaded_by, storage_key, version, scanned_status
- **GovernmentForm** — id, name, template_key
- **Authority** — id, name, contact_info
- **Contract** — id, project_id, client_id, status
- **Quotation** — id, project_id, client_id, status
- **Payment** — id, contract_id or quotation_id, amount, status
- **Workflow** — id, applies_to (project/submission/contract), stage_definitions (JSON)
- **Timeline Entry** — id, project_id, entity_type, entity_id, description, created_at (append-only, system-generated)
- **Message** — id, project_id or client_id, sender_id, body
- **Notification** — id, user_id, type, payload, read_at (nullable)
- **AuditLog** — id, user_id, action, entity_type, entity_id, before/after snapshot, created_at
- **AIHistory** — id, provider, model, prompt_hash, response, user_id, created_at

## Key Relationships

```
Client 1──* Project 1──* Task
                    1──* GovernmentSubmission
                    1──* Contract 1──* ContractMilestone
                    1──* Contract 1──* Quotation
                    1──* Document
                    1──* TimelineEntry

Task / GovernmentSubmission / ContractMilestone
        └──0..1── Escalation (polymorphic, via entity_type + entity_id)
```
