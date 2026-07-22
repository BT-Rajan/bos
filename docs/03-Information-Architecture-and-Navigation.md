# 03 - Information Architecture & Navigation

```
Login
  └── Home
        ├── Calendar (default view)
        │     ├── Day / Week / Month toggle
        │     ├── Due-item chips (task / submission / milestone, color-coded by status)
        │     └── Click item → deep-links into Workspace, in context
        │
        └── Workspace
              ├── Projects
              │     └── Project Detail
              │           ├── Overview
              │           ├── Documents
              │           ├── Government
              │           ├── Contracts
              │           ├── Quotations
              │           ├── Tasks
              │           └── Timeline
              ├── Clients
              ├── Government Center
              │     ├── Forms Library
              │     ├── Authorities
              │     └── Submissions
              ├── Contracts (cross-project list view)
              ├── Quotations (cross-project list view)
              ├── Payments
              ├── Reports
              └── Admin
                    ├── Users & Roles
                    ├── Workflows
                    ├── AI Configuration
                    └── Company Settings

Global (available from any screen):
  ├── Search
  ├── Notifications
  ├── Messages
  └── AI Assistant drawer
```

## Navigation Rules

- **Home is the only post-login landing page.** No separate "dashboard" competing with Calendar for that role.
- **Manager/admin users** see a rollup toggle on Calendar (their own items vs. team-wide) rather than a separate screen.
- **Every due item on Calendar is a direct link**, not a summary requiring a second navigation step — clicking a task due-chip opens that task inside its project's Tasks tab; clicking a submission opens Government Center pre-filtered to that submission.
- **Workspace list screens (Projects, Clients, Contracts, Quotations) share one list/table pattern** — same search bar position, same filter chip style, same pagination control — so a user who learns one learns all of them.
