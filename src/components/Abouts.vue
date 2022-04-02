<script setup>
import WindowPopup from './reusable/WindowPopup.vue'
import Accented from './reusable/Accented.vue';
import HoverSwitchText from './reusable/HoverSwitchText.vue';
import HoverSwitchImage from './reusable/HoverSwitchImage.vue';

// images to use
import pfp from '../assets/pfp.jpg'
import placeholder from '../assets/placeholder.png'

const emits = defineEmits(['closeWindow'])

function emitClose() {
  emits('closeWindow')
}
</script>

<template>
<WindowPopup window-title="About Me" @close-window="emitClose">
  <div class="about-content">
    <div class="hero">
      <div class="pfp">
        <HoverSwitchImage :ori="pfp" :hidden="placeholder"/>
      </div>
      <div class="hero-desc">
        <h1>I'm <HoverSwitchText ori="Hanyue" hidden="Xuan Bin"/></h1>
        <div>
          <p>A <Accented>student developer</Accented></p>
          <p>Based in <Accented>Penang</Accented></p>
        </div>
      </div>
    </div>
  </div>
</WindowPopup>
</template>

<style scoped>
.about-content {
  height: 100%;
  width: 100%;
  overflow: auto;
}

.hero {
  display: flex;
  justify-content: center;
  gap: 5%;
  margin-top: 6%;
}

.pfp {
  width: 20%;
  max-width: 190px;
}

.hero-desc {
  width: 65%;
  display: flex;
  flex-direction: column;
  justify-content: center;
  gap: 10%;
}

h1 {
  font-size: 3em;
}

p {
  font-size: 2em;
}
</style>