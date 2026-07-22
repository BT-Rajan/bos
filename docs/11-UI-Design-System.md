# 11 - UI Design System

A fresh visual language, not constrained by the earlier prototype's UI.

## Palette
- Neutral base (near-white surface, dark-gray text) — the interface should not compete for attention with the data on it.
- One accent color for primary actions and links.
- Status colors, used consistently everywhere status appears:
  - Not Started — neutral gray
  - In Progress — blue
  - Due Today — amber
  - Overdue — red
  - Escalated — deep red / flagged icon
  - Completed — green

## Typography
- One typeface family, two weights (regular, semibold) — hierarchy from size and weight, not from excessive borders or shadows.
- Generous line height on lists and cards for scanability.

## Core Components (design-system package, shared everywhere)
- Button (primary/secondary/destructive/ghost)
- Input, Select, Date Picker (date picker always shows both calendar-pick and typed entry)
- Table (shared pagination, sort, filter-chip pattern — same instance used by Projects, Clients, Contracts, Quotations lists)
- Card (used for Calendar due-items and dashboard-style summaries)
- Status Badge (the single source of truth for status color/label pairing)
- Modal / Drawer (AI Assistant uses the drawer pattern specifically, to stay visually distinct from system content)
- Empty State (icon + one line + optional primary action)
- Skeleton Loader (for anything expected to take >300ms)

## Calendar-Specific
- Day chip: compact, status-colored, entity-type icon (task/submission/milestone), click → deep link.
- Week/Month view: density favors legibility over cramming — a busy day shows a "+N more" rather than shrinking chips illegibly.

## Accessibility
- Status is never color-only — every status badge pairs color with a text label and, where compact, an icon.
- Keyboard navigable forms and tables.
