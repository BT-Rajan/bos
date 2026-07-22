<template>
  <div class="table-wrap">
    <div v-if="$slots.filters" class="table__filters">
      <slot name="filters" />
    </div>

    <table class="table">
      <thead>
        <tr>
          <th v-if="statusKey" class="table__rail-col" aria-hidden="true" />
          <th
            v-for="col in columns"
            :key="col.key"
            :class="{ 'table__th--sortable': col.sortable }"
            @click="col.sortable && toggleSort(col.key)"
          >
            <span class="table__th-content">
              {{ col.label }}
              <span v-if="col.sortable" class="table__sort-icon" aria-hidden="true">
                {{ sortKey === col.key ? (sortDir === "asc" ? "▲" : "▼") : "↕" }}
              </span>
            </span>
          </th>
        </tr>
      </thead>

      <tbody>
        <tr v-if="rows.length === 0">
          <td :colspan="columns.length + (statusKey ? 1 : 0)">
            <slot name="empty">
              <div class="table__empty">{{ emptyMessage }}</div>
            </slot>
          </td>
        </tr>

        <tr
          v-for="(row, i) in rows"
          :key="rowKey ? (row as any)[rowKey] : i"
          class="table__row"
          :class="statusKey ? `status-${(row as any)[statusKey]}` : null"
        >
          <td v-if="statusKey" class="table__rail-col">
            <span class="table__rail" />
          </td>
          <td v-for="col in columns" :key="col.key">
            <slot :name="`cell-${col.key}`" :row="row">
              {{ (row as any)[col.key] }}
            </slot>
          </td>
        </tr>
      </tbody>
    </table>

    <div v-if="total !== undefined" class="table__pagination">
      <span class="table__pagination-info">
        Page {{ page }} of {{ Math.max(1, Math.ceil(total / pageSize)) }} · {{ total }} total
      </span>
      <div class="table__pagination-controls">
        <button
          class="table__page-btn"
          :disabled="page <= 1"
          @click="$emit('update:page', page - 1)"
        >
          Previous
        </button>
        <button
          class="table__page-btn"
          :disabled="page >= Math.ceil(total / pageSize)"
          @click="$emit('update:page', page + 1)"
        >
          Next
        </button>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref } from "vue";

interface Column {
  key: string;
  label: string;
  sortable?: boolean;
}

withDefaults(
  defineProps<{
    columns: Column[];
    rows: Record<string, unknown>[];
    rowKey?: string;
    /** Field name on each row holding a Status value — enables the Due Rail per row. */
    statusKey?: string;
    page?: number;
    pageSize?: number;
    total?: number;
    emptyMessage?: string;
  }>(),
  { page: 1, pageSize: 20, emptyMessage: "Nothing here yet." }
);

const emit = defineEmits<{
  (e: "update:page", page: number): void;
  (e: "sort", payload: { key: string; dir: "asc" | "desc" }): void;
}>();

const sortKey = ref<string | null>(null);
const sortDir = ref<"asc" | "desc">("asc");

function toggleSort(key: string) {
  if (sortKey.value === key) {
    sortDir.value = sortDir.value === "asc" ? "desc" : "asc";
  } else {
    sortKey.value = key;
    sortDir.value = "asc";
  }
  emit("sort", { key, dir: sortDir.value });
}
</script>

<style scoped>
.table-wrap {
  display: flex;
  flex-direction: column;
  gap: var(--space-3);
}

.table__filters {
  display: flex;
  gap: var(--space-2);
  flex-wrap: wrap;
}

.table {
  width: 100%;
  border-collapse: collapse;
  background: var(--color-surface);
  border: 1px solid var(--color-line);
  border-radius: var(--radius-md);
  overflow: hidden;
  font-family: var(--font-body);
  font-size: var(--text-sm);
}

.table thead th {
  text-align: left;
  font-weight: var(--weight-medium);
  color: var(--color-ink-soft);
  padding: var(--space-3) var(--space-4);
  border-bottom: 1px solid var(--color-line);
  background: var(--color-bg);
  white-space: nowrap;
}

.table__th--sortable {
  cursor: pointer;
  user-select: none;
}

.table__th-content {
  display: inline-flex;
  align-items: center;
  gap: var(--space-1);
}

.table__sort-icon {
  font-size: var(--text-xs);
  color: var(--color-ink-soft);
}

.table__row td {
  padding: var(--space-3) var(--space-4);
  border-bottom: 1px solid var(--color-line);
  color: var(--color-ink);
}

.table__row:last-child td {
  border-bottom: none;
}

.table__row:hover td {
  background: var(--color-bg);
}

/* Due Rail per row — same signature element as Card, applied at row scope */
.table__rail-col {
  width: var(--rail-width);
  padding: 0 !important;
}

.table__rail {
  display: block;
  width: var(--rail-width);
  align-self: stretch;
  height: 100%;
  background: var(--status-color, transparent);
}

.table__empty {
  text-align: center;
  color: var(--color-ink-soft);
  padding: var(--space-8);
}

.table__pagination {
  display: flex;
  align-items: center;
  justify-content: space-between;
  font-size: var(--text-xs);
  color: var(--color-ink-soft);
}

.table__pagination-controls {
  display: flex;
  gap: var(--space-2);
}

.table__page-btn {
  font-family: var(--font-body);
  font-size: var(--text-xs);
  padding: var(--space-1) var(--space-3);
  border: 1px solid var(--color-line-strong);
  border-radius: var(--radius-sm);
  background: var(--color-surface);
  cursor: pointer;
}

.table__page-btn:disabled {
  opacity: 0.4;
  cursor: not-allowed;
}

.table__page-btn:not(:disabled):hover {
  border-color: var(--color-accent);
  color: var(--color-accent);
}
</style>
