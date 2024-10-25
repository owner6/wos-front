<script setup lang="ts">
defineProps<{
  game: {
    tokens: number;
    crystals: number;
    energy: number;
    health: number;
  }
}>();
</script>

<template>
  <div class="game-header">
    <div class="stats">
      <span>🪙 {{ game.tokens.toFixed(0) }}</span>
      <span>💎 {{ game.crystals.toFixed(3) }}</span>
      <span>⚡ {{ game.energy.toFixed(2) }}</span>
    </div>
    <div class="health-bar">
      <div :style="{ width: game.health + '%' }" class="health-fill"></div>
    </div>
  </div>
</template>

<style scoped>
.game-header {
  background-color: #2a2a2a;
  padding: 1rem;
  margin-bottom: 1rem;
}

.stats {
  display: flex;
  gap: 1rem;
  margin-bottom: 0.5rem;
}

.health-bar {
  width: 100%;
  height: 20px;
  background-color: #444;
  border-radius: 4px;
  overflow: hidden;
}

.health-fill {
  height: 100%;
  background-color: #4caf50;
  transition: width 0.3s ease;
}
</style>