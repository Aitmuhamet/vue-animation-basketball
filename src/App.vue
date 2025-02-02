<script setup>
import BasketballScoreboard from './components/BasketballScoreboard.vue'
</script>

<template>
  <div class="app-inner">
    <BasketballScoreboard />
  </div>
</template>

<style>
#app {
  max-width: unset;
  padding: 0;
  width: 100vw;
}

.app-inner {
  display: flex;
  justify-content: center;

  height: 100%;
  aspect-ratio: 16 / 9;
  background: rgb(0, 120, 0);
}
</style>
