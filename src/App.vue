<script setup lang="ts">
import TickTackToe from './views/TickTackToe.vue'
</script>

<template>
  <header>
    <h1>Tick-Tack-Toe</h1>
  </header>
  <main>
    <TickTackToe />
  </main>
</template>

<style lang="css" scoped>
header {
  text-align: center;
  margin-bottom: 2rem;
}
main {
  display: flex;
  align-items: center;
  justify-content: center;
}
</style>
