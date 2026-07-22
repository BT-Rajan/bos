<template>
  <Teleport to="body">
    <Transition name="modal-fade">
      <div v-if="modelValue" class="modal-overlay" @mousedown.self="close">
        <div
          class="modal"
          role="dialog"
          aria-modal="true"
          :aria-label="title"
          @keydown.esc="close"
        >
          <header class="modal__header">
            <h2 class="modal__title">{{ title }}</h2>
            <button class="modal__close" aria-label="Close" @click="close">✕</button>
          </header>

          <div class="modal__body">
            <slot />
          </div>

          <footer v-if="$slots.footer" class="modal__footer">
            <slot name="footer" />
          </footer>
        </div>
      </div>
    </Transition>
  </Teleport>
</template>

<script setup lang="ts">
const props = defineProps<{ modelValue: boolean; title: string }>();
const emit = defineEmits<{ (e: "update:modelValue", value: boolean): void }>();

function close() {
  emit("update:modelValue", false);
}
void props;
</script>

<style scoped>
.modal-overlay {
  position: fixed;
  inset: 0;
  background: rgba(28, 36, 48, 0.45);
  display: flex;
  align-items: center;
  justify-content: center;
  padding: var(--space-4);
  z-index: 100;
}

.modal {
  background: var(--color-surface);
  border-radius: var(--radius-lg);
  box-shadow: var(--shadow-md);
  width: 100%;
  max-width: 560px;
  max-height: 90vh;
  display: flex;
  flex-direction: column;
}

.modal__header {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: var(--space-5) var(--space-6);
  border-bottom: 1px solid var(--color-line);
}

.modal__title {
  font-family: var(--font-display);
  font-size: var(--text-lg);
  font-weight: var(--weight-semibold);
  color: var(--color-ink);
  margin: 0;
}

.modal__close {
  background: none;
  border: none;
  color: var(--color-ink-soft);
  font-size: var(--text-base);
  cursor: pointer;
  padding: var(--space-1);
  line-height: 1;
}

.modal__close:hover {
  color: var(--color-ink);
}

.modal__body {
  padding: var(--space-6);
  overflow-y: auto;
  font-family: var(--font-body);
  font-size: var(--text-sm);
  color: var(--color-ink);
}

.modal__footer {
  padding: var(--space-4) var(--space-6);
  border-top: 1px solid var(--color-line);
  display: flex;
  justify-content: flex-end;
  gap: var(--space-3);
}

.modal-fade-enter-active,
.modal-fade-leave-active {
  transition: opacity var(--duration-base) var(--ease-standard);
}
.modal-fade-enter-from,
.modal-fade-leave-to {
  opacity: 0;
}
</style>
