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
    <h1 id="title">Viewing: {{ windowTitle }}</h1>
    <span id="close" @click="emitClose">X CLOSE</span>
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
  grid-template-columns: 6fr 4fr;
  align-items: center;
  margin: 0 auto;
  padding: 2vh 0px 1vh 0px;
  border-bottom: 2px solid var(--accent);
}

#title {
  height: fit-content;
}

#close {
  font-size: 2em;
  margin-left: auto;
  width: auto;
  padding: 5px 18px;
  text-align: center;
  color: var(--error);
  cursor: pointer;
  transition: .3s ease;
  border-radius: 15px;
  border: 2px solid var(--error)
}

#close:hover {
  background-color: var(--error);
  color: var(--text-color);
}

.content {
  height: 90%;
  width: 90%;
  margin: 0 auto;
  margin-top: 1vh;
}
</style>