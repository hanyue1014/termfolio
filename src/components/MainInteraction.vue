<script setup>
import Input from './Input.vue';
import OutputDiv from './OutputDiv.vue';

defineProps(['commands'])

const emit = defineEmits(['run-command'])

function sendCommand(command) {
  emit('run-command', command)
}
</script>

<template>
<div class="vert-grid">
  <OutputDiv :commands="commands"/>
  <Input @run-command="sendCommand" />
</div>
</template>

<style scoped>
.vert-grid {
  display: grid;
  grid-template-rows: 9fr 1fr;
  row-gap: 3vh;
}

.output-container {
  display: flex;
  align-items: center;
  background-color: var(--div-bg);
  border-radius: 25px;
  padding: 2vh 2vw;
}

.output {
  overflow-y: auto;
  height: 68vh;
  /* padding-right: 1vw; */
  width: 100%;
}

.output p {
  font-size: 1.5em;
  margin-top: 1vh;
}

.blinking-cursor {
  width: 1ch;
  color: var(--accent);  /* to hide the text inside the span element */
  background-color: var(--accent);
  animation: blinking-caret .5s linear infinite alternate;
}

@keyframes blinking-caret {
  from {
    opacity: 0;
  }
  to {
    opacity: 1;
  }
}
</style>