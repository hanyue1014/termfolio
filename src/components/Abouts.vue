<script setup>
import WindowPopup from './reusable/WindowPopup.vue'

const emits = defineEmits(['closeWindow'])

function emitClose() {
  emits('closeWindow')
}
</script>

<template>
<WindowPopup window-title="About Me" @close-window="emitClose">
  <div class="about-content">Test</div>
</WindowPopup>
</template>

<style scoped>
.about-content {
  height: 100%;
  width: 100%;
  overflow: auto;
}
</style>