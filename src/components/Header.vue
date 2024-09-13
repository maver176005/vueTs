<template>
  <header class="header">
    <div class="header-content">
      <h1>Мой склад</h1>
      <button class="report-button">
        <img src="../assets/icon-report.svg" alt="Report Icon" class="report-icon">
        Настройки отчёта
      </button>
    </div>
    <p class="item-count">Товаров: <span class="highlight">134 шт.</span></p>
  </header>
</template>

<script lang="ts">
export default {};
</script>

<style scoped>
.header {
  background-color: #fff;
  padding: 20px 36px;
  border-radius: 8px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
  display: flex;
  flex-direction: column;
}

.header-content {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

h1 {
  margin: 0;
  font-size: 36px;
  color: #333;
}

.report-button {
  display: flex;
  align-items: center;
  background-color: transparent;
  border: 1px solid #a4b7d9;
  border-radius: 6px;
  color: #6a7b96;
  font-size: 14px;
  padding: 8px 12px;
  cursor: pointer;
  transition: background-color 0.3s ease;
}

.report-button:hover {
  background-color: #e0e9ff;
}

.report-icon {
  width: 16px;
  height: 16px;
  margin-right: 8px;
}

.item-count {
  margin-top: 10px;
  font-size: 24px;
  color: #666;
}

.highlight {
  color: #f75b5b;
  font-weight: bold;
}
</style>
