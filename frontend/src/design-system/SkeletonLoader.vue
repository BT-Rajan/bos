<template>
  <span
    class="skeleton"
    :class="`skeleton--${shape}`"
    :style="{ width, height }"
    aria-hidden="true"
  />
</template>

<script setup lang="ts">
withDefaults(
  defineProps<{
    shape?: "text" | "rect" | "circle";
    width?: string;
    height?: string;
  }>(),
  { shape: "text", width: "100%", height: "1em" }
);
</script>

<style scoped>
.skeleton {
  display: inline-block;
  background: linear-gradient(
    90deg,
    var(--color-line) 25%,
    var(--color-line-strong) 37%,
    var(--color-line) 63%
  );
  background-size: 400% 100%;
  animation: skeleton-shimmer 1.4s ease-in-out infinite;
}

.skeleton--text {
  border-radius: var(--radius-sm);
}

.skeleton--rect {
  border-radius: var(--radius-md);
}

.skeleton--circle {
  border-radius: 50%;
}

@keyframes skeleton-shimmer {
  0% { background-position: 100% 50%; }
  100% { background-position: 0 50%; }
}

@media (prefers-reduced-motion: reduce) {
  .skeleton {
    animation: none;
    background: var(--color-line);
  }
}
</style>
