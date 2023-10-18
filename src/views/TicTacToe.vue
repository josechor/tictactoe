<script lang="ts" setup>
import { ref, type Ref } from 'vue'

const turnos: Ref<number> = ref(0)
const tablero: Ref<string[]> = ref(['', '', '', '', '', '', '', '', ''])
const resultado: Ref<string> = ref('')
const finished: Ref<boolean> = ref(false)

function handleClick(n: number) {
  if (finished.value) return
  const player = jugador()
  if (comprobarCasilla(n)) {
    return
  }
  tablero.value[n] = player
  turnos.value++
  if (checkWin()) {
    finished.value = true
    setTimeout(() => {
      resultado.value = `Ganador: ${player}`
    }, 1)
  }
  if (turnos.value === 9) {
    finished.value = true
    setTimeout(() => {
      resultado.value = `Empate`
    }, 1)
  }
}
function comprobarCasilla(n: number) {
  if (tablero.value[n] !== '') {
    alert('Casilla ocupada')
    return true
  }
  return false
}
function checkWin() {
  return (
    (tablero.value[0] === tablero.value[1] &&
      tablero.value[1] === tablero.value[2] &&
      tablero.value[0] !== '') ||
    (tablero.value[3] === tablero.value[4] &&
      tablero.value[4] === tablero.value[5] &&
      tablero.value[3] !== '') ||
    (tablero.value[6] === tablero.value[7] &&
      tablero.value[7] === tablero.value[8] &&
      tablero.value[6] !== '') ||
    (tablero.value[0] === tablero.value[3] &&
      tablero.value[3] === tablero.value[6] &&
      tablero.value[0] !== '') ||
    (tablero.value[1] === tablero.value[4] &&
      tablero.value[4] === tablero.value[7] &&
      tablero.value[1] !== '') ||
    (tablero.value[2] === tablero.value[5] &&
      tablero.value[5] === tablero.value[8] &&
      tablero.value[2] !== '') ||
    (tablero.value[0] === tablero.value[4] &&
      tablero.value[4] === tablero.value[8] &&
      tablero.value[0] !== '') ||
    (tablero.value[2] === tablero.value[4] &&
      tablero.value[4] === tablero.value[6] &&
      tablero.value[2] !== '')
  )
}

function jugador() {
  return turnos.value % 2 === 0 ? 'X' : 'O'
}

function reset() {
  turnos.value = 0
  tablero.value = ['', '', '', '', '', '', '', '', '']
  resultado.value = ''
  finished.value = false
}
</script>

<template>
  <section>
    <article class="tablero">
      <div
        class="casilla"
        v-for="(casilla, index) in tablero"
        :key="index"
        @click="handleClick(index)"
      >
        {{ casilla }}
      </div>
      <article class="resultado" :class="{ mostrar: resultado !== '' }">{{ resultado }}</article>
    </article>
    <footer>
      <div class="activePlayer">
        <span class="player" :class="{ active: jugador() === 'X' }">X</span>
        <span class="player" :class="{ active: jugador() === 'O' }">O</span>
      </div>
      <button class="reset" @click="reset()">Reiniciar</button>
    </footer>
  </section>
</template>

<style lang="css" scoped>
section {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  gap: 20px;
}
.resultado {
  z-index: -1;
  opacity: 0;
  position: absolute;
  width: 100%;
  height: 100%;
  top: 0;
  left: 0;
  background: #0000007e;
  color: white;
  align-items: center;
  justify-content: center;
  font-size: 35px;
  backdrop-filter: blur(5px);
  display: flex;
  transition: all 0.2s ease;
}
.mostrar {
  opacity: 1;
  z-index: 1;
}
footer {
  flex-direction: column;
  gap: 10px;
  display: flex;
  justify-content: center;
  align-items: center;
}
.reset {
  padding: 10px 16px;
  border-radius: 16px;
  border: none;
  outline: none;
  background-color: #40798c;
  color: white;
  font-size: 20px;
  font-weight: 600;
  cursor: pointer;
  transition: all 0.1s ease;
}
.reset:hover {
  background-color: #70a9a1;
  color: #cfe0c3;
  transform: rotateZ(3deg);
}
.activePlayer {
  display: flex;
  justify-content: space-around;
}
.player {
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 40px;
  font-weight: 600;
  margin-top: 10px;
  border-radius: 16px;
  transition: all 0.1s ease;
  width: fit-content;
  aspect-ratio: 1/1;
  padding: 0px 10px;
}
.active {
  color: #cfe0c3;
  background-color: #40798c;
}
.tablero {
  position: relative;
  display: grid;
  grid-template-columns: 1fr 1fr 1fr;
  gap: 0;
  width: fit-content;
}
.casilla {
  position: relative;
  color: #70a9a1;
  width: 100px;
  height: 100px;
  display: inline-block;
  cursor: pointer;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 50px;
  font-weight: 700;
  transition: background 0.2s ease;
}
.casilla:hover {
  background: rgb(13, 42, 51);
}
.casilla:nth-child(1),
.casilla:nth-child(2),
.casilla:nth-child(4),
.casilla:nth-child(5) {
  border-right: 4px solid #70a9a1;
  border-bottom: 4px solid #70a9a1;
}
.casilla:nth-child(3),
.casilla:nth-child(6) {
  border-bottom: 4px solid #70a9a1;
}

.casilla:nth-child(7),
.casilla:nth-child(8) {
  border-right: 4px solid #70a9a1;
}
</style>
