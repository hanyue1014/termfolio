<script setup>
import { onMounted, shallowRef } from 'vue';
import Accented from './Accented.vue';
import LsOutputVue from '../LsOutput.vue';
import WindowOutput from './WindowOutput.vue';

const props = defineProps(['commandToRun'])
const emit = defineEmits(['scrollDown'])

const commandOutput = shallowRef(null)

switch (props.commandToRun.trim()) {
  case 'about':
    commandOutput.value = WindowOutput
    break
  case 'skills':
    commandOutput.value = WindowOutput
    break
  case 'projects':
    commandOutput.value = WindowOutput
    break
  case 'contacts':
    commandOutput.value = WindowOutput
    break
  case 'ls -Rl':
    commandOutput.value = LsOutputVue
    break
  case 'ls -lR':
    commandOutput.value = LsOutputVue
    break
  default:
    commandOutput.value = null
}

// tell the parent's container to scroll after this component is mounted and visible
onMounted(() => {
  emit('scrollDown')
})
</script>

<template>
<p>$ <Accented>{{ commandToRun.trim() }}</Accented></p>
<p v-if="!commandOutput">unknown command: <Accented>{{ commandToRun.trim() }}</Accented></p>
<component v-else-if="commandOutput != LsOutputVue" 
  :is="commandOutput" 
  :command-ran="commandToRun.trim()" />
<component v-else :is="commandOutput" />
</template>

<style scoped>
p {
  font-size: 1.5em;
  margin-top: 1vh;
}
</style>