# 01 - Product Vision & UX Principles

## Vision

A small engineering consultancy shouldn't need a project manager whose whole job is "did we miss anything." BOS makes the answer to that question visible the moment someone logs in, without requiring anyone to go looking for it.

## UX Principles (crisp, not decorative)

1. **One glance answers "what do I need to do today."** Home (Calendar) is the default landing view, not a dashboard of charts nobody reads.
2. **Nothing disappears silently.** Overdue items stay visible until a person acts — complete, follow up, reschedule, or escalate. The system never quietly drops something off the list.
3. **Minimum clicks to depth.** Calendar → click a due item → land directly inside the relevant project/submission/contract, in context. No intermediate "here's a list, now go find it" step.
4. **Plain layouts over dense ones.** Favor whitespace, clear hierarchy, and one primary action per screen over cramming every possible control into view. Advanced/rare actions live one level deeper, not on the main surface.
5. **Status is always color- and label-coded consistently** across Calendar, Workspace, and every list view — On Track / Due Today / Overdue / Escalated / Completed use the same colors everywhere, no per-module reinvention.
6. **Forms ask for what's needed, not everything the data model supports.** Optional fields are collapsed by default; required fields (like a task's completion date) are never optional in the UI even if the database happens to allow null.
7. **The AI assistant is a drawer, not a takeover.** It suggests; it never blocks or replaces a human decision, and it's visually distinct from system-of-record content so a user always knows what's a suggestion versus a fact.
8. **Consistent empty and loading states.** Every list/table has a designed empty state ("No tasks due today — nice") rather than a blank screen, and skeleton loaders rather than spinners for anything that takes more than ~300ms.

## Design Language (see 11-UI-Design-System.md for specifics)

- Restrained palette: neutral base, a small set of status colors, one accent color for primary actions.
- Typography-led hierarchy over heavy borders/boxes.
- Cards and tables kept visually quiet so status colors and due dates — the things that matter — stand out.
