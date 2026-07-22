# 00 - Overview

**Product:** BOS (Business Operating System) for Almailam Engineering Consultants
**Repo:** BT-Rajan/bos
**Nature of this repo:** Unified — frontend and backend live and are documented together, built as one tightly-connected system rather than a frontend consuming a loosely-coupled API.

## What BOS Is

BOS replaces the module-browsing model of the earlier prototype (`almailam-roadmap-ui`) with a **due-date-driven** model:

- Every user's day starts at **Home**, split into **Calendar** and **Workspace**.
- **Calendar** answers "what's due, what's overdue, what needs a decision" — aggregated across tasks, government submission deadlines, and contract milestones.
- **Workspace** holds everything else — Projects, Clients, Documents, Government Center, Contracts, Quotations, Payments, Reports, Admin — all the depth of the original prototype, unchanged in function, reorganized in entry point.
- Anything due and not completed becomes **Overdue**, and stays visibly overdue until a person follows up, reschedules, completes it late, or escalates it. Nothing silently disappears.

## Why "Tightly Connected"

This system deliberately shares one escalation/calendar engine across tasks, government submissions, and contract milestones, and keeps frontend and backend documented and versioned together in one repo. This trades some modular independence for less code, faster iteration, and one place to reason about "what's due" — the right trade for a single-product, 10-20 person team. See `06-Architecture.md` for the specific consequences of this choice.

## Doc Index

| Doc | Covers |
|---|---|
| 01 | Product vision & UX principles |
| 02 | Full functional scope — every function, nothing dropped from the original prototype |
| 03 | Information architecture & navigation |
| 04 | Unified data model |
| 05 | API reference |
| 06 | Architecture (tightly-connected rationale, layering, repo structure) |
| 07 | Calendar & Escalation Engine spec (the shared core) |
| 08 | AI behaviour rules |
| 09 | Security & compliance |
| 10 | Performance & scalability |
| 11 | UI design system |
| 12 | Coding standards |
| 13 | Testing strategy |
| 14 | Deployment & operations (no containers) |
| 15 | Pass plan (build order) |
| 16 | Effort estimate |
