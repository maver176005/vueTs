<template>
  <div class="editable-value">
    <div v-if="!isEditing" @click="startEditing" class="value-display">
      {{ value }} шт.
    </div>

    <div v-else class="editing-controls">
      <input v-model="newValue" type="number" class="input-field" />
      <button @click="save" class="icon-button save-button">

        <svg width="20" height="20" viewBox="0 0 20 20" fill="none" xmlns="http://www.w3.org/2000/svg">
          <rect width="20" height="20" rx="4" fill="#5068A5"/>
          <path d="M5 9.17391L8.91304 13.087L15 7" stroke="white" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/>
        </svg>

      </button>
      <button @click="cancel" class="icon-button cancel-button">

        <svg width="20" height="20" viewBox="0 0 20 20" fill="none" xmlns="http://www.w3.org/2000/svg">
          <rect x="0.5" y="0.5" width="19" height="19" rx="3.5" stroke="#D8DCE9"/>
          <path d="M5.5 5.5L14.5 14.5" stroke="#5068A5"/>
          <path d="M14.5 5.5L5.5 14.5" stroke="#5068A5"/>
        </svg>

      </button>
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent, ref } from 'vue';

export default defineComponent({
  name: 'EditableValue',
  props: {
    value: {
      type: Number,
      required: true
    }
  },
  setup(props, { emit }) {
    const isEditing = ref(false); // Состояние редактирования
    const newValue = ref(props.value); // Значение для редактирования

    const startEditing = () => {
      isEditing.value = true;
      newValue.value = props.value; // Инициализируем ввод текущим значением
    };

    const save = () => {
      isEditing.value = false;
      emit('update:value', newValue.value); // Отправляем новое значение
    };

    const cancel = () => {
      isEditing.value = false;
      newValue.value = props.value; // Отмена изменений
    };

    return {
      isEditing,
      newValue,
      startEditing,
      save,
      cancel
    };
  }
});
</script>

<style scoped>
.editable-value {
  display: inline-block;
}

.value-display {
  cursor: pointer;
  font-weight: bold;
  font-size: 16px;
  color: #4A4A4A;
  text-align: center;
  padding: 5px;
  background-color: rgba(255, 255, 255, 0);
  border-radius: 4px;

}

.editing-controls {
  display: flex;
  align-items: center;
}

.input-field {
  width: 60px;
  padding: 5px;
  font-size: 16px;
  border: 1px solid #CCC;
  border-radius: 4px;
}

.icon-button {
  background-color: transparent;
  border: none;
  cursor: pointer;
  margin-left: 8px;
}

.icon-button svg {
  width: 20px;
  height: 20px;
  color: #007bff;
}

.save-button svg {
  color: #28a745;
}

.cancel-button svg {
  color: #dc3545;
}

.icon-button:hover svg {
  color: #0056b3;
}
</style>
