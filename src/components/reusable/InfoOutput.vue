<script setup>
import { onMounted } from 'vue';
import Accented from './Accented.vue';

const props = defineProps(['commandToRun'])
const emit = defineEmits(['scrollDown'])

console.log(props.commandToRun)

// tell the parent's container to scroll after this component is mounted and visible
onMounted(() => {
  emit('scrollDown')
})
</script>

<template>
<p>$ <Accented>{{ props.commandToRun }}</Accented></p>
<p>unknown command: <Accented>{{ props.commandToRun }}</Accented></p>
</template>

<style scoped>
p {
  font-size: 1.5em;
  margin-top: 1vh;
}
</style>