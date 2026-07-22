<template>
  <label class="field" :class="{ 'field--error': !!error }">
    <span v-if="label" class="field__label">
      {{ label }}<span v-if="required" class="field__required" aria-hidden="true"> *</span>
    </span>

    <span class="field__control">
      <input
        class="field__input"
        :type="type"
        :value="modelValue"
        :placeholder="placeholder"
        :disabled="disabled"
        :required="required"
        @input="$emit('update:modelValue', ($event.target as HTMLInputElement).value)"
      />
    </span>

    <span v-if="error" class="field__error">{{ error }}</span>
    <span v-else-if="hint" class="field__hint">{{ hint }}</span>
  </label>
</template>

<script setup lang="ts">
withDefaults(
  defineProps<{
    modelValue?: string;
    label?: string;
    placeholder?: string;
    type?: "text" | "email" | "password" | "number" | "date" | "tel";
    required?: boolean;
    disabled?: boolean;
    error?: string;
    hint?: string;
  }>(),
  { type: "text", required: false, disabled: false }
);

defineEmits<{ (e: "update:modelValue", value: string): void }>();
</script>

<style scoped>
.field {
  display: flex;
  flex-direction: column;
  gap: var(--space-1);
  font-family: var(--font-body);
}

.field__label {
  font-size: var(--text-sm);
  font-weight: var(--weight-medium);
  color: var(--color-ink);
}

.field__required {
  color: var(--color-danger);
}

.field__control {
  display: block;
}

.field__input {
  width: 100%;
  font-family: var(--font-body);
  font-size: var(--text-base);
  color: var(--color-ink);
  background: var(--color-surface);
  border: 1px solid var(--color-line-strong);
  border-radius: var(--radius-sm);
  padding: var(--space-2) var(--space-3);
  transition: border-color var(--duration-fast) var(--ease-standard),
    box-shadow var(--duration-fast) var(--ease-standard);
}

.field__input::placeholder {
  color: var(--color-ink-soft);
  opacity: 0.6;
}

.field__input:focus {
  outline: none;
  border-color: var(--color-accent);
  box-shadow: 0 0 0 3px var(--color-focus-ring);
}

.field__input:disabled {
  background: var(--color-bg);
  cursor: not-allowed;
  opacity: 0.6;
}

.field--error .field__input {
  border-color: var(--color-danger);
}

.field__error {
  font-size: var(--text-xs);
  color: var(--color-danger);
}

.field__hint {
  font-size: var(--text-xs);
  color: var(--color-ink-soft);
}
</style>
