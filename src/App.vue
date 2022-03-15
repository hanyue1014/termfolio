<script setup>
import { ref } from 'vue';
import Landing from './components/Landing.vue'
import Main from './components/Main.vue'

let waitInteraction = ref(true)

function addListenerForNextPhase() {
  // directly let the window capture any interactions
  window.addEventListener('keypress', nextPhase)
  window.addEventListener('mousedown', nextPhase)
}

function nextPhase() {
  waitInteraction.value = !waitInteraction.value
  window.removeEventListener('mousedown', nextPhase)
  window.removeEventListener('keypress', nextPhase)
}
</script>

<template>
<Transition name="landing">
  <Landing v-if="waitInteraction" @add-listener="addListenerForNextPhase"/>
</Transition>
<Transition name="nextphase">
  <Main v-if="!waitInteraction" />
</Transition>
</template>

<style>
@import url('https://fonts.googleapis.com/css2?family=Ubuntu+Mono&display=swap');

:root {
  --text-color: hsla(156, 100%, 90%, 100%);
  --accent: hsla(179, 88%, 46%, 100%);
  --div-bg: hsla(204, 88%, 23%, 100%);
  --bg: hsla(246, 71%, 14%, 100%);
}

* {
  margin: 0;
  padding: 0;
  transform-origin: center;
}

#app {
  font-family: 'Ubuntu Mono', monospace;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  background: var(--bg);
  color: var(--text-color);
  min-height: 100vh;
  margin: 0;
  padding: 0;
}

/* For the transition of the divs */
.landing-enter-active,
.landing-leave-active {
  transition: all 0.5s ease;
}

.landing-enter-from,
.landing-leave-to {
  transform: scale(1.5, 1.5);
  opacity: 0;
}

.nextphase-enter-active,
.nextphase-leave-active {
  transition: all 0.5s ease;
}

.nextphase-enter-from,
.nextphase-leave-to {
  transform: scale(0, 0);
  opacity: 0;
}
</style>
