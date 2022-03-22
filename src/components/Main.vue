<script setup>
import { ref } from 'vue';

import Header from './Header.vue'
import Commands from './Commands.vue';
import MainInteraction from './MainInteraction.vue';

const commands = ref([])

function sendToOutput(command) {
  commands.value.push(command)
}
</script>

<template>
<div class="container">
  <Header />
  <div  class="command-section-container">
    <MainInteraction :commands="commands" @run-command="sendToOutput" />
    <Commands @run-command="sendToOutput" />
  </div>
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
</style>