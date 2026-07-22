# Design Plan — F1

**Subject:** a due-date accountability tool for a Kuwait-based engineering consultancy. The people using it daily are engineers and coordinators tracking government deadlines and contract milestones — not consumers. The page's job: make "what's due, what's late" impossible to miss, everywhere, without shouting.

## Palette (named)

| Name | Hex | Use |
|---|---|---|
| Slate Ink | `#1C2430` | Primary text |
| Fog | `#F6F7F9` | App background |
| Paper | `#FFFFFF` | Card/surface background |
| Line | `#E2E5EA` | Borders, dividers |
| Drafting Teal | `#0F6E6E` | Primary accent — actions, links, focus ring |
| Amber Flag | `#D97706` | Due Today |
| Signal Red | `#DC2626` | Overdue |
| Escalation Crimson | `#7F1D1D` | Escalated |
| Moss | `#15803D` | Completed |
| Slate Muted | `#94A3B8` | Not Started |

Rejected the cream/serif/terracotta look and the near-black/acid-accent look deliberately — this is a working tool used for hours a day, not a marketing page; it needs to recede and let status color carry the signal. Drafting Teal was chosen over blue because it reads calmer at high information density (many status chips visible at once) and doesn't clash with the red/amber/crimson status scale the way a standard blue does.

## Type

- **Display / section headers:** Space Grotesk — geometric, slightly technical, drafting-table character without being decorative. Used sparingly: page titles, empty-state headlines.
- **Body / UI:** Inter — dense-data legibility, the workhorse for tables, forms, labels.
- **Utility / data:** IBM Plex Mono — dates, IDs, timestamps, due-date countdowns. Monospacing makes date columns scannable at a glance, which matters directly for this product's job.

## Layout Concept

Quiet surfaces (Fog background, Paper cards, hairline Line borders), status color reserved almost exclusively for the signature element below — everything else stays deliberately neutral so status never has to compete for attention.

## Signature Element — the Due Rail

A 4px colored rail on the left edge of every row/card that carries a due date (task, calendar chip, submission, milestone) — colored by status (Muted/Teal-tinted-blue for In Progress/Amber/Red/Crimson/Moss). It's a literal margin-flag, the way an engineer would mark up a drawing — turning an abstract status enum into a spatial, always-visible marker that reads the same way on a Calendar day, a Project's task list, or a Government submission row. This is the one place status color and a strong visual device combine; everywhere else stays quiet by comparison.

## Self-Critique

First pass had the rail on *every* component including buttons — cut that; the rail belongs only to due-date-bearing rows/cards, not to controls, so it keeps its meaning instead of becoming decoration.
