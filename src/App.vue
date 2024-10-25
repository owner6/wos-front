<script setup lang="ts">
import { ref, onMounted, onUnmounted } from 'vue';
import GameHeader from './components/GameHeader.vue';
import GameMenu from './components/GameMenu.vue';
import Storage from './components/Storage.vue';
import Battle from './components/Battle.vue';

const game = ref({
  tokens: 0,
  tokenGrowth: 9.978070175438596,
  tokensUpgLevel: 1,
  crystals: 0,
  crystalGrowth: 0.0060032894736842,
  crystalsUpgLevel: 0,
  energy: 7280,
  energyGrowth: 4.989035087719298,
  fightLimit: 3,
  health: 100,
  healthGrowth: 2.5,
  water: 0,
  waterGrowth: 0.180,
  waterUpgLevel: 1,
  rawChicken: 0,
  friedChicken: 0,
  dieselFuel: 0,
  scrapMetal: 0,
  lightNoiseGrenade: 0
});

const showStorage = ref(false);

let timer: number;

onMounted(() => {
  loadGame();
  timer = setInterval(() => {
    endOfTurnCalc();
    saveGame();
  }, 3600000); // 1 hour
});

onUnmounted(() => {
  clearInterval(timer);
});

function endOfTurnCalc() {
  if (game.value.energy >= 2.796) {
    game.value.tokens += game.value.tokenGrowth * game.value.tokensUpgLevel;
    game.value.crystals += game.value.crystalGrowth * game.value.crystalsUpgLevel;
    game.value.energy -= game.value.energyGrowth;
    game.value.health = Math.min(100, game.value.health + game.value.healthGrowth);
    game.value.fightLimit = Math.min(3, game.value.fightLimit + 1);
    game.value.water += game.value.waterGrowth * game.value.waterUpgLevel;
  }
}

function saveGame() {
  localStorage.setItem('gameTutorial', JSON.stringify(game.value));
}

function loadGame() {
  const savedGame = localStorage.getItem('gameTutorial');
  if (savedGame) {
    game.value = JSON.parse(savedGame);
  }
}

function toggleStorage() {
  showStorage.value = !showStorage.value;
}
</script>

<template>
  <div class="game-container">
    <GameHeader :game="game" />
    <GameMenu />
    <button @click="toggleStorage">{{ showStorage ? 'Закрити склад' : 'Відкрити склад' }}</button>
    <Storage v-if="showStorage" :game="game" />
    <Battle :game="game" />
  </div>
</template>

<style>
.game-container {
  background-color: #1a1a1a;
  color: #fff;
  min-height: 100vh;
  padding: 1rem;
}

button {
  background-color: #c17c17;
  color: white;
  border: none;
  padding: 0.5rem 1rem;
  cursor: pointer;
  margin: 0.5rem;
}

button:hover {
  background-color: #a66915;
}
</style>