<template>
  <Teleport to="body">
    <Transition name="drawer-fade">
      <div v-if="modelValue" class="drawer-overlay" @mousedown.self="close">
        <Transition name="drawer-slide" appear>
          <aside
            v-if="modelValue"
            class="drawer"
            :class="{ 'drawer--accent': accent }"
            role="dialog"
            aria-modal="true"
            :aria-label="title"
            @keydown.esc="close"
          >
            <header class="drawer__header">
              <span v-if="accent" class="drawer__badge">AI Suggestion</span>
              <h2 class="drawer__title">{{ title }}</h2>
              <button class="drawer__close" aria-label="Close" @click="close">✕</button>
            </header>

            <div class="drawer__body">
              <slot />
            </div>

            <footer v-if="$slots.footer" class="drawer__footer">
              <slot name="footer" />
            </footer>
          </aside>
        </Transition>
      </div>
    </Transition>
  </Teleport>
</template>

<script setup lang="ts">
withDefaults(
  defineProps<{
    modelValue: boolean;
    title: string;
    /** Reserved for the AI Assistant drawer specifically — applies the tinted
     * treatment that keeps AI suggestions visually distinct from system-of-record
     * content (see 01-Product-Vision-and-UX-Principles.md). Don't set this on
     * ordinary utility drawers. */
    accent?: boolean;
  }>(),
  { accent: false }
);

const emit = defineEmits<{ (e: "update:modelValue", value: boolean): void }>();

function close() {
  emit("update:modelValue", false);
}
</script>

<style scoped>
.drawer-overlay {
  position: fixed;
  inset: 0;
  background: rgba(28, 36, 48, 0.25);
  z-index: 100;
  display: flex;
  justify-content: flex-end;
}

.drawer {
  width: min(420px, 100%);
  height: 100%;
  background: var(--color-surface);
  box-shadow: var(--shadow-md);
  display: flex;
  flex-direction: column;
  border-left: 1px solid var(--color-line);
}

/* AI-only treatment: soft teal wash + accent-colored left edge, so the whole
   panel reads as "suggestion," never mistaken for editable system content. */
.drawer--accent {
  background: linear-gradient(180deg, var(--color-accent-soft) 0%, var(--color-surface) 140px);
  border-left: 3px solid var(--color-accent);
}

.drawer__header {
  padding: var(--space-5) var(--space-6);
  border-bottom: 1px solid var(--color-line);
  display: flex;
  flex-direction: column;
  gap: var(--space-1);
  position: relative;
}

.drawer__badge {
  font-family: var(--font-body);
  font-size: var(--text-xs);
  font-weight: var(--weight-semibold);
  color: var(--color-accent);
  text-transform: uppercase;
  letter-spacing: 0.04em;
}

.drawer__title {
  font-family: var(--font-display);
  font-size: var(--text-lg);
  font-weight: var(--weight-semibold);
  color: var(--color-ink);
  margin: 0;
}

.drawer__close {
  position: absolute;
  top: var(--space-5);
  right: var(--space-6);
  background: none;
  border: none;
  color: var(--color-ink-soft);
  font-size: var(--text-base);
  cursor: pointer;
}

.drawer__close:hover {
  color: var(--color-ink);
}

.drawer__body {
  flex: 1;
  overflow-y: auto;
  padding: var(--space-6);
  font-family: var(--font-body);
  font-size: var(--text-sm);
  color: var(--color-ink);
}

.drawer__footer {
  padding: var(--space-4) var(--space-6);
  border-top: 1px solid var(--color-line);
}

.drawer-fade-enter-active,
.drawer-fade-leave-active {
  transition: opacity var(--duration-base) var(--ease-standard);
}
.drawer-fade-enter-from,
.drawer-fade-leave-to {
  opacity: 0;
}

.drawer-slide-enter-active,
.drawer-slide-leave-active {
  transition: transform var(--duration-base) var(--ease-standard);
}
.drawer-slide-enter-from,
.drawer-slide-leave-to {
  transform: translateX(100%);
}
</style>
