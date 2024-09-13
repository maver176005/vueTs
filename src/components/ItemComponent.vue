<template>
  <div class="item-container">
    <div class="item-header">
      <img :src="image" alt="Item Image" class="item-image" />
      <h3>{{ itemName }}</h3>
    </div>

    <button @click="toggleDetails" class="toggle-button">
      {{ showDetails ? 'Свернуть размерный ряд' : 'Развернуть размерный ряд' }}
    </button>

    <table v-if="showDetails" class="item-details">
      <thead>
      <tr>
        <th>Размер</th>
        <th>Остаток WB</th>
        <th>Хватин на</th>
        <th>Остаток у поставщика</th>
        <th>Хватит на</th>
        <th>Остаток мой склад</th>
        <th>Хватит на</th>
        <th>В пути от производителя</th>
        <th>Скорость заказов</th>
        <th>История изменений</th>
      </tr>
      </thead>
      <tbody>
      <tr v-for="detail in details" :key="detail.size">

        <td>
          <div class="size-box">{{ detail.size }}</div>
        </td>
        <td>
          <EditableValue :value="detail.stockWB" @update:value="updateDetail(detail, 'stockWB', $event)" />
        </td>
        <td>
          <EditableValue :value="detail.daysWB" @update:value="updateDetail(detail, 'daysWB', $event)" />
        </td>
        <td>
          <EditableValue :value="detail.stockSupplier" @update:value="updateDetail(detail, 'stockSupplier', $event)" />
        </td>
        <td>
          <EditableValue :value="detail.daysSupplier" @update:value="updateDetail(detail, 'daysSupplier', $event)" />
        </td>
        <td>
          <EditableValue :value="detail.stockWarehouse" @update:value="updateDetail(detail, 'stockWarehouse', $event)" />
        </td>
        <td>
          <EditableValue :value="detail.daysWarehouse" @update:value="updateDetail(detail, 'daysWarehouse', $event)" />
        </td>
        <td>
          <EditableValue :value="detail.inTransit" @update:value="updateDetail(detail, 'inTransit', $event)" />
        </td>
        <td>
          <EditableValue :value="detail.orderSpeed" @update:value="updateDetail(detail, 'orderSpeed', $event)" />
        </td>
        <td>
          <button class="view-button" @click="viewItem(itemName)">Посмотреть</button>
        </td>
      </tr>
      </tbody>
    </table>
  </div>
</template>

<script lang="ts">
import { defineComponent, ref } from 'vue';
import EditableValue from './EditableValue.vue';
import type { Detail } from './MainContent.vue';

export default defineComponent({
  name: 'ItemComponent',
  components: {
    EditableValue,
  },
  props: {
    itemName: {
      type: String,
      required: true,
    },
    details: {
      type: Array as () => Detail[],
      required: true,
    },
    image: {
      type: String,
      required: true,
    },
  },
  setup() {
    const showDetails = ref(false);
    const toggleDetails = () => {
      showDetails.value = !showDetails.value;
    };
    const viewItem = (name: string) => {
      alert(`Посмотреть детали товара: ${name}`);
    };
    const updateDetail = (detail: Detail, field: keyof Detail, value: number) => {
      detail[field] = value;
    };

    return { showDetails, toggleDetails, viewItem, updateDetail };
  },
});
</script>

<style scoped>
.item-container {
  border: 1px solid #ddd;
  padding: 20px;
  border-radius: 8px;
  background-color: white;
}

.item-header {
  display: flex;
  align-items: center;
}

.item-image {
  width: 60px;
  height: 60px;
  object-fit: cover;
  margin-right: 20px;
}

.item-details {
  width: 1100px;
  border-collapse: collapse;
  margin-top: 20px;
}

.item-details td,
.item-details th {
  border-left: none;
  border-right: none;
  height: 60px;
  border-top: 1px solid #ddd;
  border-bottom: 1px solid #ddd;
  font: 14px 'Lato', sans-serif;
}

.item-details th {
  background-color: #f4f4f4;
  border: none;
}


.size-box {
  background-color: #ff69b4;
  color: white;
  font-weight: bold;
  width: 40px;
  height: 40px;
  display: flex;
  justify-content: center;
  align-items: center;
  border-radius: 10px;
}

.view-button {
  background-color: #5068a5;
  color: white;
  border: none;
  padding: 5px 10px;
  border-radius: 4px;
  cursor: pointer;
}

.view-button:hover {
  background-color: #0056b3;
}

.toggle-button {
  margin-top: 10px;
  padding: 5px 15px;
  background-color: #007bff;
  color: white;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}

.toggle-button:hover {
  background-color: #0056b3;
}
</style>
