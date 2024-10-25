<template>
  <div class="menu">
    <button class="menu-item">ДІМ</button>
    <button class="menu-item">БЕЗПЕЧНА ЗОНА</button>
    <button class="menu-item">ПОКИНУТІ ЗЕМЛІ</button>
    <button class="menu-item">КУХНЯ</button>
    <button class="menu-item">МАЙСТЕРНЯ</button>
    <button class="menu-item">ОБМІННИК</button>
    <button class="menu-item">ЛАВКА</button>
  </div>
</template>

<style scoped>
.menu {
  display: flex;
  flex-direction: column;
  gap: 0.5rem;
}

.menu-item {
  background-color: #c17c17;
  color: white;
  border: none;
  padding: 1rem;
  cursor: pointer;
  text-align: center;
  font-weight: bold;
}

.menu-item:hover {
  background-color: #a66915;
}
</style>