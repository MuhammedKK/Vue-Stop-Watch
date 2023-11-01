<script setup lang="ts">
import { ref } from 'vue';

const timerState = ref<"running" | "stopped" | 'pauesd'>('stopped')
const timeRef = ref(0);
const interval = ref<number | undefined>(undefined)

const start = () => {
  timerState.value = "running"
  interval.value = setInterval(() => {
    timeRef.value++
  }, 1000)
};

const pause = () => {
  timerState.value = "pauesd"
  clearInterval(interval.value)
}

const restart = () => {
  timeRef.value = 0
  timerState.value = "running"
  if(interval.value !== undefined) {
    clearInterval(interval.value);
    interval.value = undefined
  }
  start();
}
</script>

<template>
  <div>
    <div>{{timeRef}}</div>
    <button v-if='timerState === "stopped"' @click="start">Start</button>
    <button v-if='timerState === "running"' @click="pause">Pause</button>
    <button @click="start">Resume</button>
    <button @click="restart">Restart</button>
  </div>
</template>

<style scoped>
</style>
