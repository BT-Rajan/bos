<template>
  <button
    class="btn"
    :class="[`btn--${variant}`, `btn--${size}`, { 'btn--loading': loading }]"
    :disabled="disabled || loading"
    :type="type"
    @click="$emit('click', $event)"
  >
    <span v-if="loading" class="btn__spinner" aria-hidden="true" />
    <span class="btn__label"><slot /></span>
  </button>
</template>

<script setup lang="ts">
withDefaults(
  defineProps<{
    variant?: "primary" | "secondary" | "destructive" | "ghost";
    size?: "sm" | "md" | "lg";
    type?: "button" | "submit";
    disabled?: boolean;
    loading?: boolean;
  }>(),
  {
    variant: "primary",
    size: "md",
    type: "button",
    disabled: false,
    loading: false,
  }
);

defineEmits<{ (e: "click", ev: MouseEvent): void }>();
</script>

<style scoped>
.btn {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  gap: var(--space-2);
  font-family: var(--font-body);
  font-weight: var(--weight-medium);
  border-radius: var(--radius-sm);
  border: 1px solid transparent;
  cursor: pointer;
  transition: background-color var(--duration-fast) var(--ease-standard),
    border-color var(--duration-fast) var(--ease-standard),
    box-shadow var(--duration-fast) var(--ease-standard);
  white-space: nowrap;
}

.btn:focus-visible {
  outline: none;
  box-shadow: 0 0 0 3px var(--color-focus-ring);
}

.btn:disabled {
  cursor: not-allowed;
  opacity: 0.5;
}

/* Sizes */
.btn--sm { font-size: var(--text-sm); padding: var(--space-1) var(--space-3); }
.btn--md { font-size: var(--text-base); padding: var(--space-2) var(--space-4); }
.btn--lg { font-size: var(--text-lg); padding: var(--space-3) var(--space-6); }

/* Variants */
.btn--primary {
  background: var(--color-accent);
  color: var(--color-surface);
}
.btn--primary:not(:disabled):hover { background: var(--color-accent-hover); }

.btn--secondary {
  background: var(--color-surface);
  color: var(--color-ink);
  border-color: var(--color-line-strong);
}
.btn--secondary:not(:disabled):hover { border-color: var(--color-accent); }

.btn--destructive {
  background: var(--color-danger);
  color: var(--color-surface);
}
.btn--destructive:not(:disabled):hover { background: var(--color-danger-hover); }

.btn--ghost {
  background: transparent;
  color: var(--color-ink-soft);
}
.btn--ghost:not(:disabled):hover {
  background: var(--color-bg);
  color: var(--color-ink);
}

.btn__spinner {
  width: 14px;
  height: 14px;
  border: 2px solid currentColor;
  border-right-color: transparent;
  border-radius: 50%;
  animation: btn-spin 600ms linear infinite;
}

@keyframes btn-spin {
  to { transform: rotate(360deg); }
}
</style>
