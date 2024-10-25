<script setup lang="ts">
defineProps<{
  game: {
    water: number;
    rawChicken: number;
    friedChicken: number;
    dieselFuel: number;
    scrapMetal: number;
    lightNoiseGrenade: number;
  }
}>();
</script>

<template>
  <div class="storage">
    <h2>Склад</h2>
    <div class="storage-items">
      <div class="item">Вода: {{ game.water.toFixed(3) }}</div>
      <div class="item">Сире куряче м'ясо: {{ game.rawChicken }}</div>
      <div class="item">Жарене куряче м'ясо: {{ game.friedChicken }}</div>
      <div class="item">Дизельне паливо: {{ game.dieselFuel }}</div>
      <div class="item">Металобрухт: {{ game.scrapMetal }}</div>
      <div class="item">Світлошумова граната: {{ game.lightNoiseGrenade }}</div>
    </div>
  </div>
</template>

<style scoped>
.storage {
  background-color: #2a2a2a;
  padding: 1rem;
  margin: 1rem 0;
  border-radius: 4px;
}

.storage-items {
  display: grid;
  gap: 0.5rem;
}

.item {
  padding: 0.5rem;
  background-color: #333;
  border-radius: 4px;
}
</style>