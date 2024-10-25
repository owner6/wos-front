<script setup lang="ts">
import { ref } from 'vue';

const props = defineProps<{
  game: {
    health: number;
    energy: number;
    fightLimit: number;
    lightNoiseGrenade: number;
    rawChicken: number;
    tokens: number;
    tokenGrowth: number;
  }
}>();

const enemyHealth = ref(25);
const playerDamage = 4;
const playerDamageGranate = 20;
const enemyDamage = 5;
const canRun = ref(true);
const battleResult = ref('');

function resetBattle() {
  enemyHealth.value = 25;
  battleResult.value = '';
}

function attack() {
  if (!canRun.value || props.game.energy <= 0 || props.game.fightLimit < 1) {
    return;
  }

  canRun.value = false;
  setTimeout(() => { canRun.value = true; }, 2000);

  // Player attack
  enemyHealth.value -= Math.floor(Math.random() * playerDamage) + 1;

  if (enemyHealth.value <= 0) {
    props.game.rawChicken += Math.floor(Math.random() * 2) + 1;
    props.game.energy -= 1;
    props.game.fightLimit -= 1;
    battleResult.value = 'Ви перемогли!';
    setTimeout(resetBattle, 2000);
    return;
  }

  // Enemy attack
  props.game.health -= Math.floor(Math.random() * enemyDamage) + 1;

  if (props.game.health <= 0) {
    props.game.tokens -= Math.floor(Math.random() * 2) + props.game.tokenGrowth;
    props.game.energy -= 1;
    props.game.fightLimit -= 1;
    battleResult.value = 'Ви програли!';
    setTimeout(resetBattle, 2000);
  }
}
</script>

<template>
  <div class="battle">
    <div class="battle-stats">
      <div>Здоров'я ворога: {{ enemyHealth }}</div>
      <div>Ліміт боїв: {{ game.fightLimit }}</div>
    </div>
    <div class="battle-controls">
      <button @click="attack" :disabled="!canRun || game.energy <= 0 || game.fightLimit < 1">
        Атакувати
      </button>
    </div>
    <div v-if="battleResult" class="battle-result">
      {{ battleResult }}
    </div>
  </div>
</template>

<style scoped>
.battle {
  background-color: #2a2a2a;
  padding: 1rem;
  margin: 1rem 0;
  border-radius: 4px;
}

.battle-stats {
  margin-bottom: 1rem;
}

.battle-result {
  margin-top: 1rem;
  font-weight: bold;
  color: #4caf50;
}

button:disabled {
  background-color: #666;
  cursor: not-allowed;
}
</style>