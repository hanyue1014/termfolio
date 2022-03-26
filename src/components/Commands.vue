<script setup>
import CommandBtn from './reusable/CommandBtn.vue';

const emit = defineEmits(['runCommand'])

const btnCommands = ['about', 'contacts', 'skills', 'ls -Rl']

function sendCommand(command) {
  emit('runCommand', command)
}
</script>

<template>
<div class="commands">
  <h1>Commands</h1>
  <div class="command-btns">
    <CommandBtn 
      v-for="command in btnCommands"
      :btn-text="command" 
      @run-command="sendCommand" />
  </div>
</div>
</template>

<style scoped>
.commands {
  padding: 5vh 2vw;
  border-radius: 25px;
  background: var(--div-bg);
}

h1 {
  text-align: center;
  font-size: 2.25em;
}

.command-btns {
  display: flex;
  flex-direction: column;
  margin-top: 45%;
}
</style>