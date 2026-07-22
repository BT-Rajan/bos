<template>
  <div class="card" :class="[status ? `status-${status}` : null, { 'card--railed': !!status }]">
    <header v-if="$slots.header || title" class="card__header">
      <slot name="header">
        <h3 class="card__title">{{ title }}</h3>
      </slot>
      <StatusBadge v-if="status" :status="status" />
    </header>

    <div class="card__body">
      <slot />
    </div>

    <footer v-if="$slots.footer" class="card__footer">
      <slot name="footer" />
    </footer>
  </div>
</template>

<script setup lang="ts">
import StatusBadge, { type Status } from "./StatusBadge.vue";

defineProps<{
  title?: string;
  /** When set, renders the Due Rail — reserved for content that carries a due date
   * (tasks, government submissions, contract milestones). Do not use on generic cards. */
  status?: Status;
}>();
</script>

<style scoped>
.card {
  background: var(--color-surface);
  border: 1px solid var(--color-line);
  border-radius: var(--radius-md);
  box-shadow: var(--shadow-sm);
  padding: var(--space-4);
  display: flex;
  flex-direction: column;
  gap: var(--space-3);
}

/* The Due Rail — the signature element, reserved for due-date-bearing content */
.card--railed {
  border-left: var(--rail-width) solid var(--status-color);
  padding-left: calc(var(--space-4) - var(--rail-width) + var(--space-1));
}

.card__header {
  display: flex;
  align-items: flex-start;
  justify-content: space-between;
  gap: var(--space-3);
}

.card__title {
  font-family: var(--font-display);
  font-size: var(--text-lg);
  font-weight: var(--weight-semibold);
  color: var(--color-ink);
  margin: 0;
}

.card__body {
  font-family: var(--font-body);
  font-size: var(--text-sm);
  color: var(--color-ink-soft);
  line-height: var(--leading-normal);
}

.card__footer {
  padding-top: var(--space-3);
  border-top: 1px solid var(--color-line);
}
</style>
