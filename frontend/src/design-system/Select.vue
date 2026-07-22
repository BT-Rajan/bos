<template>
  <label class="field" :class="{ 'field--error': !!error }">
    <span v-if="label" class="field__label">
      {{ label }}<span v-if="required" class="field__required" aria-hidden="true"> *</span>
    </span>

    <span class="select__control">
      <select
        class="select__input"
        :value="modelValue"
        :disabled="disabled"
        :required="required"
        @change="$emit('update:modelValue', ($event.target as HTMLSelectElement).value)"
      >
        <option v-if="placeholder" value="" disabled>{{ placeholder }}</option>
        <option v-for="opt in options" :key="opt.value" :value="opt.value">
          {{ opt.label }}
        </option>
      </select>
      <span class="select__chevron" aria-hidden="true">▾</span>
    </span>

    <span v-if="error" class="field__error">{{ error }}</span>
    <span v-else-if="hint" class="field__hint">{{ hint }}</span>
  </label>
</template>

<script setup lang="ts">
interface Option {
  value: string;
  label: string;
}

withDefaults(
  defineProps<{
    modelValue?: string;
    label?: string;
    placeholder?: string;
    options: Option[];
    required?: boolean;
    disabled?: boolean;
    error?: string;
    hint?: string;
  }>(),
  { required: false, disabled: false }
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

.select__control {
  position: relative;
  display: block;
}

.select__input {
  width: 100%;
  appearance: none;
  font-family: var(--font-body);
  font-size: var(--text-base);
  color: var(--color-ink);
  background: var(--color-surface);
  border: 1px solid var(--color-line-strong);
  border-radius: var(--radius-sm);
  padding: var(--space-2) var(--space-8) var(--space-2) var(--space-3);
  transition: border-color var(--duration-fast) var(--ease-standard),
    box-shadow var(--duration-fast) var(--ease-standard);
}

.select__input:focus {
  outline: none;
  border-color: var(--color-accent);
  box-shadow: 0 0 0 3px var(--color-focus-ring);
}

.select__input:disabled {
  background: var(--color-bg);
  cursor: not-allowed;
  opacity: 0.6;
}

.select__chevron {
  position: absolute;
  right: var(--space-3);
  top: 50%;
  transform: translateY(-50%);
  color: var(--color-ink-soft);
  pointer-events: none;
  font-size: var(--text-sm);
}

.field--error .select__input {
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
