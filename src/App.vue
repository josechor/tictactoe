<script setup lang="ts">
import TickTackToe from './views/TickTackToe.vue'
</script>

<template>
  <div>
    <header>
      <h1>Tick-Tack-Toe</h1>
    </header>
    <main>
      <TickTackToe />
    </main>
  </div>
</template>

<style lang="css" scoped>
h1 {
  font-size: 50px;
  font-weight: 900;
  color: #70a9a1;
}
div {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  height: 100vh;
}
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
