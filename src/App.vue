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
}

.app-inner {
  width: 100vw;
  aspect-ratio: 16 / 9;
  background: rgb(0, 120, 0);
}
</style>
