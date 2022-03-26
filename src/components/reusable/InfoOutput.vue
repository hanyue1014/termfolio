<script setup>
import { onMounted, shallowRef } from 'vue';
import Accented from './Accented.vue';
import LsOutputVue from './LsOutput.vue';

const props = defineProps(['commandToRun'])
const emit = defineEmits(['scrollDown'])

const commandOutput = shallowRef(null)

switch (props.commandToRun.trim()) {
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
<component v-else :is="commandOutput" />
</template>

<style scoped>
p {
  font-size: 1.5em;
  margin-top: 1vh;
}
</style>