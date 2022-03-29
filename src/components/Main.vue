<script setup>
import { ref, shallowRef } from 'vue';

import Header from './Header.vue'
import Commands from './Commands.vue';
import MainInteraction from './MainInteraction.vue';
import About from './Abouts.vue'

const commands = ref([])

const windowOpened = shallowRef(null)

function openPopup(type) {
  if (type === 'about') {
    windowOpened.value = About
  }
  // do ntg if the command wan open eh stff is unknown
}

function sendToOutput(command) {
  commands.value.push(command)
  openPopup(command)
}

function closeWindow() {
  windowOpened.value = null
}
</script>

<template>
<div class="container">
  <Header />
  <div  class="command-section-container">
    <MainInteraction :commands="commands" @run-command="sendToOutput" />
    <Commands @run-command="sendToOutput" />
  </div>
  <Transition name="window">
    <component :is="windowOpened" @close-window="closeWindow"></component>
  </Transition>
</div>
</template>

<style scoped>
.container {
  display: grid;
  grid-template-rows: 1fr 10fr;
  margin: 0 10vw;
  height: 100vh;
}

.command-section-container {
  display: grid;
  grid-template-columns: 7fr 3fr;
  margin: 2vh 0;
  gap: 3vw;
}

/* For the transition of the divs */
.window-enter-active,
.window-leave-active {
  transition: all 0.5s ease;
}

.window-enter-from,
.window-leave-to {
  opacity: 0;
}
</style>