<script setup>
import Accented from './Accented.vue';

const props = defineProps(['commandRan'])
</script>

<template>
<p>Running Command <Accented>{{ commandRan }}</Accented></p>
<p>Window Opened.</p>
</template>

<style scoped>
p {
  font-size: 1.5em;
  margin-top: 1vh;
}
</style>