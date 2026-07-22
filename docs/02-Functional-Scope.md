# 02 - Functional Scope

Every function below existed in the original `almailam-roadmap-ui` prototype (or was added by the Calendar/Workspace pivot). This is the checklist against which "nothing missing" is verified — each item must map to a pass in `15-Pass-Plan.md` and a section in `05-API-Reference.md`.

## Home
- Post-login landing split: **Calendar** and **Workspace**.
- Calendar aggregates due items across Tasks, Government Submissions, Contract Milestones.
- Manager/admin rollup view: team-wide overdue/escalated items.

## Auth & Users
- Login, logout, refresh token, password reset.
- Role-based access (Admin, Engineer, Government Liaison, Finance, Read-only, or as confirmed with the client).
- User profile management, role assignment.

## Company
- Company-wide settings (single tenant): name, branding, contact info, defaults.

## Clients
- Client list, search, filter.
- Client detail: profile, contacts, linked projects.
- Create/edit/archive client.

## Projects (Workspace core)
- Project list, search, filter, status.
- Project detail workspace with tabs: Overview, Documents, Government, Contracts, Quotations, Tasks, Timeline/Activity.
- Create/edit/archive project.
- Project-level activity feed (Timeline).

## Tasks
- Create/edit/list tasks, scoped to a project.
- **Required** tentative completion date.
- Status lifecycle: Not Started → In Progress → Due Today → Overdue → Escalated → Completed.
- "My Tasks" view (current user, across all projects).
- Follow-up / reschedule / escalate actions on overdue tasks.

## Documents
- Upload, list, download, delete (soft-delete/versioned).
- Versioning — new upload of the same document creates a version, not an overwrite.
- Virus/malware scan before a document is marked available.
- Signed, time-limited download links.
- Encryption at rest for stored files.

## Government Center
- Government forms library (list, view, download templates).
- Authorities directory (list, contact info).
- Government submissions: create, track status, **deadline** field.
- Submissions feed into Calendar and the shared escalation engine.

## Contracts
- Create/edit contracts, link to project/client.
- Contract milestones with milestone dates — feed into Calendar and escalation.
- AI-assisted draft/rewrite/summarize (see 08-AI-Behaviour.md).

## Quotations
- Create/edit/list quotations, link to client/project.
- Status tracking (draft/sent/accepted/rejected).

## Payments
- Record/track payments against contracts/quotations.
- Payment status.
- Payment gateway webhook handling.

## Workflows
- Admin-configurable stage definitions (used by Projects, Government Submissions, Contracts as applicable).

## Timeline
- Per-project activity feed — automatically populated by actions across modules (task created, document uploaded, submission filed, etc.), not manually maintained.

## Messages
- Internal messaging tied to a project or client context.

## Notifications
- In-app notification feed, read/unread state, preferences.
- Escalation notifications (task/submission/milestone overdue → assignee's manager).

## Search
- Global search across Clients, Projects, Documents, Tasks, Government Submissions.

## AI Assistant
- Config-driven, swappable provider (Claude / DeepSeek / future).
- Draft/summarize/rewrite assistance in Documents, Contracts, Government submissions, Customer Communication.
- Standard response envelope (summary, details, confidence, suggested actions) regardless of provider.
- No write access to system-of-record data — suggestions only.
- Full history log of every AI call.

## Reports
- Dashboard-style reports: project status, overdue/escalation trends, financial summary (quotations/payments), government submission compliance.
- AI-generated executive summaries.

## Admin
- Users & roles, Workflows, Government forms library, AI configuration, Company settings — all wired into one admin area.

## Customer Portal (public, unauthenticated)
- Status tracker: mobile number + project ID → project status/timeline only. No sensitive data exposed. Rate-limited.

## Cross-Cutting (not a module, but required everywhere)
- Audit log on every write (who, what, when).
- Timezone-correct due-date/overdue evaluation (Asia/Kuwait business timezone).
- Consistent status color/label coding across all of the above.
