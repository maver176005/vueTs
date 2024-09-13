<template>
  <div class="main-content">
    <FilterPanel :filters="filters" :activeFilter="activeFilter" @setFilter="setFilter" />
    <section class="items">
      <ItemComponent
          v-for="item in filteredItems"
          :key="item.name"
          :itemName="item.name"
          :details="item.details"
          :image="item.image"
      />
    </section>
  </div>
</template>

<script lang="ts">
import { defineComponent, ref, computed } from 'vue';
import ItemComponent from './ItemComponent.vue';
import FilterPanel from './FilterPanel.vue';

export interface Detail {
  size: number;
  stockWB: string;
  daysWB: number;
  stockSupplier: string;
  daysSupplier: number;
  stockWarehouse: string;
  daysWarehouse: number;
  inTransit: string;
  orderSpeed: string;
  history: string[];
}

export interface Item {
  name: string;
  details: Detail[];
  image: string;
}

export default defineComponent({
  name: 'MainContent',
  components: {
    ItemComponent,
    FilterPanel
  },
  setup() {

    const items = ref<Item[]>([
      {
        name: 'Долговечный букет из 9 роз в коробке',
        image: 'src/assets/rose_box.png', //изображение
        details: [
          {
            size: 38,
            stockWB: '55 475 ',
            daysWB: 4,
            stockSupplier: '1 000 ',
            daysSupplier: 5,
            stockWarehouse: '11 453 ',
            daysWarehouse: 6,
            inTransit: '453 ',
            orderSpeed: '5 шт./день',
            history: ['Изменение 1', 'Изменение 2']
          },
          {
            size: 88,
            stockWB: '55 475 ',
            daysWB: 4,
            stockSupplier: '1 000 ',
            daysSupplier: 5,
            stockWarehouse: '11 453 ',
            daysWarehouse: 6,
            inTransit: '453 ',
            orderSpeed: '5 шт./день',
            history: ['Изменение 1', 'Изменение 2']
          },
          {
            size: 11,
            stockWB: '55 475 ',
            daysWB: 4,
            stockSupplier: '1 000 ',
            daysSupplier: 5,
            stockWarehouse: '11 453 ',
            daysWarehouse: 6,
            inTransit: '453 ',
            orderSpeed: '5 шт./день',
            history: ['Изменение 1', 'Изменение 2']
          }
        ]
      },
      {
        name: 'Композиция из свежих цветов',
        image: 'src/assets/rose_box.png',
        details: [
          {
            size: 42,
            stockWB: '30 500 ',
            daysWB: 3,
            stockSupplier: '500 ',
            daysSupplier: 4,
            stockWarehouse: '7 200 ',
            daysWarehouse: 5,
            inTransit: '200 ',
            orderSpeed: '8 шт./день',
            history: ['Изменение 1', 'Изменение 3']
          }
        ]
      },
      {
        name: 'Букет из искусственных лилий',
        image: 'src/assets/rose_box.png',
        details: [
          {
            size: 50,
            stockWB: '22 100',
            daysWB: 2,
            stockSupplier: '1 200 ',
            daysSupplier: 6,
            stockWarehouse: '5 000 ',
            daysWarehouse: 7,
            inTransit: '300 ',
            orderSpeed: '10 шт./день',
            history: ['Изменение 2', 'Изменение 4']
          }
        ]
      },


    ]);


    // Фильтры
    const filters = ref([
      { name: 'stockWB', label: 'Остаток на WB' },
      { name: 'stockSupplier', label: 'Остаток у поставщика' },
      { name: 'stockWarehouse', label: 'Остаток на складе' },
      { name: 'inTransit', label: 'В пути от производителя' }
    ]);

    // Активный фильтр по умолчанию
    const activeFilter = ref('stockWB');

    // Метод для изменения активного фильтра
    const setFilter = (filterName: string) => {
      activeFilter.value = filterName;
    };

    // Отфильтрованные товары на основе активного фильтра
    const filteredItems = computed(() => {
      return items.value.filter(item => {
        // Пример логики фильтрации: отбираем товары, где данные по выбранному фильтру не пустые
        return item.details.some(detail => !!detail[activeFilter.value as keyof Detail]);
      });
    });

    return {
      items,
      filters,
      activeFilter,
      setFilter,
      filteredItems
    };
  }
});
</script>

<style scoped>
.main-content {
  padding: 20px;
}

.items {
  width: 100%;
  display: flex;
  flex-direction: column;
  gap: 20px;
}
</style>
