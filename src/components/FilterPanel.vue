<template>
  <div class="filter-panel">
    <div class="filters">
      <button
          v-for="filter in filters"
          :key="filter.name"
          :class="{ active: activeFilter === filter.name }"
          @click="setFilter(filter.name)"
      >
        {{ filter.label }}
      </button>
    </div>
    <div class="actions">
      <span>История заказов</span>
      <span>Скорость заказов: 7 дней</span>
      <span>Интервал заказов</span>
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent, ref } from 'vue';

export default defineComponent({
  name: 'FilterPanel',
  setup() {
    const filters = ref([
      { name: 'stockWB', label: 'Остаток на WB' },
      { name: 'stockSupplier', label: 'Остаток у поставщика' },
      { name: 'stockWarehouse', label: 'Остаток на складе' },
      { name: 'inTransit', label: 'В пути от производителя' }
    ]);
    const activeFilter = ref('stockWB');

    const setFilter = (filterName: string) => {
      activeFilter.value = filterName;
    };

    return {
      filters,
      activeFilter,
      setFilter
    };
  }
});
</script>

<style scoped>
.filter-panel {
  display: flex;
  justify-content: space-between;
  align-items: center;
  background-color: #f0f4ff;
  padding: 12px 24px;
  border-radius: 8px;
  margin-bottom: 20px;
  border: 1px solid #d0d8f0;
}

.filters {
  display: flex;
  gap: 10px;
}

.filters button {
  background-color: transparent;
  border: none;
  color: #6a7b96;
  font-size: 14px;
  cursor: pointer;
}

.filters button.active {
  color: #1e3a8a;
  font-weight: bold;
}

.actions {
  display: flex;
  gap: 20px;
  color: #6a7b96;
  font-size: 14px;
}
</style>
