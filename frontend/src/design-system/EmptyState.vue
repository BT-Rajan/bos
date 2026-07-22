<template>
  <div class="empty-state">
    <div class="empty-state__icon" aria-hidden="true">
      <slot name="icon">◌</slot>
    </div>
    <p class="empty-state__message">{{ message }}</p>
    <Button v-if="actionLabel" variant="secondary" size="sm" @click="$emit('action')">
      {{ actionLabel }}
    </Button>
  </div>
</template>

<script setup lang="ts">
import Button from "./Button.vue";

defineProps<{
  /** Written from the end user's side — what's true right now, plainly stated.
   * e.g. "No tasks due today — nice." not "No data available." */
  message: string;
  actionLabel?: string;
}>();

defineEmits<{ (e: "action"): void }>();
</script>

<style scoped>
.empty-state {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  gap: var(--space-3);
  padding: var(--space-12) var(--space-6);
  text-align: center;
}

.empty-state__icon {
  font-size: var(--text-2xl);
  color: var(--color-line-strong);
}

.empty-state__message {
  font-family: var(--font-body);
  font-size: var(--text-sm);
  color: var(--color-ink-soft);
  margin: 0;
  max-width: 32ch;
}
</style>
