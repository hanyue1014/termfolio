<script setup>
import WindowPopup from './reusable/WindowPopup.vue'

const emits = defineEmits(['closeWindow'])

function emitClose() {
  emits('closeWindow')
}
</script>

<template>
<WindowPopup window-title="Contacts" @close-window="emitClose">

</WindowPopup>
</template>

<style scoped>
</style>