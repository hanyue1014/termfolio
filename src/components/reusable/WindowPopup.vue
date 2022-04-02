<script setup>
defineProps(['windowTitle'])
const emits = defineEmits(['closeWindow'])

function emitClose() {
  emits('closeWindow')
}
</script>

<template>
<div class="popup">
  <div class="title">
    <h1 id="title">{{ windowTitle }}</h1>
    <span id="close" @click="emitClose">&times;</span>
  </div>
  <div class="content">
    <slot></slot>
  </div>
</div>
</template>

<style>
.popup {
  /* center the popup */
  position: absolute;
  z-index: 80;  /* make the pop up appear over anything else */
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);

  width: 75vw;
  height: 90vh;
  background-color: hsla(246, 71%, 14%, 85%);
  border-radius: 25px;
}

.title {
  display: grid;
  width: 90%;
  grid-template-columns: 10fr 1fr;
  align-items: center;
  margin: 0 auto;
  padding: 2vh 0px 1vh 0px;
  border-bottom: 2px solid var(--accent);
}

#title {
  height: fit-content;
}

#close {
  font-size: 2.5em;
  margin-left: auto;
  width: 50%;
  text-align: center;
  cursor: pointer;
  transition: .3s ease;
  border-radius: 10px;
}

#close:hover {
  background-color: var(--error);
}

.content {
  height: 90%;
  width: 90%;
  margin: 0 auto;
  margin-top: 1vh;
}
</style>