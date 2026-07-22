<template>
  <span class="status-badge" :class="statusClass">
    <span class="status-badge__dot" aria-hidden="true" />
    <span class="status-badge__label">{{ label }}</span>
  </span>
</template>

<script setup lang="ts">
import { computed } from "vue";

export type Status =
  | "not_started"
  | "in_progress"
  | "due_today"
  | "overdue"
  | "escalated"
  | "completed";

const LABELS: Record<Status, string> = {
  not_started: "Not Started",
  in_progress: "In Progress",
  due_today: "Due Today",
  overdue: "Overdue",
  escalated: "Escalated",
  completed: "Completed",
};

const props = defineProps<{ status: Status }>();

const statusClass = computed(() => `status-${props.status}`);
const label = computed(() => LABELS[props.status]);
</script>

<style scoped>
/* Status color is set per-status via the .status-* utility classes
   defined once in tokens.css (--status-color custom property). */
.status-badge {
  display: inline-flex;
  align-items: center;
  gap: var(--space-2);
  font-family: var(--font-body);
  font-size: var(--text-xs);
  font-weight: var(--weight-medium);
  color: var(--color-ink-soft);
  padding: var(--space-1) var(--space-2);
  border-radius: var(--radius-sm);
  background: var(--color-bg);
  white-space: nowrap;
}

.status-badge__dot {
  width: 8px;
  height: 8px;
  border-radius: 50%;
  background: var(--status-color);
  flex-shrink: 0;
}

/* Escalated additionally gets bold text — never rely on color alone. */
.status-escalated .status-badge__label {
  font-weight: var(--weight-semibold);
  color: var(--status-color);
}
</style>
