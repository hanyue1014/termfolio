<script setup>
import { ref, onMounted } from 'vue';
import Accented from './reusable/Accented.vue';

let h1El = ref(null)

let pEl = ref(null)

let keyCapturer = ref(null)

let emit = defineEmits(['addListener'])

onMounted(() => {
  console.log(h1El.value, pEl.value)

  // do h1's typing animation first
  let [h1_width, h1_maxWidth] = [0, h1El.value.textContent.length]
  let h1_lastTime = null

  let [p_width, p_maxWidth] = [0, pEl.value.textContent.length]
  let p_lastTime = null

  let pElAnim = time => {
    if (!p_lastTime) {
      p_lastTime = time

      // initialise the blinking caret animation
      pEl.value.style.borderRightColor = 'hsla(179, 88%, 46%, 100%)'
      pEl.value.style.animationPlayState = 'running'
    }

    if (p_width < p_maxWidth) {
      // i wan the words come out .1s (this content longer) per word
      if ((time - p_lastTime) / 1000 >= 0.1 ) {
        p_lastTime = time
        pEl.value.style.width = ++p_width + 'ch'
      }
      window.requestAnimationFrame(pElAnim)
    } else {
      // p element typing animation done
      // tell parent to start listening to user's interaction
      emit('addListener')
    }
  }

  let h1ElAnim = time => {
    if (!h1_lastTime) {
      h1_lastTime = time

      // initialise the blinking caret animation
      h1El.value.style.borderRightColor = 'hsla(179, 88%, 46%, 100%)'
      h1El.value.style.animationPlayState = 'running'
    }

    if (h1_width < h1_maxWidth) {
      // i wan the words come out .15s per word
      if ((time - h1_lastTime) / 1000 >= 0.15 ) {
        h1_lastTime = time
        h1El.value.style.width = ++h1_width + 'ch'
      }
      window.requestAnimationFrame(h1ElAnim)
    } else {
      // stop h1's blinking caret
      h1El.value.style.animationPlayState = 'paused'
      h1El.value.style.borderRightStyle = 'none'
      // width is alrd bigger than maxWidth, the animation ended, can run p's animation d
      window.requestAnimationFrame(pElAnim)
    }
  }

  window.requestAnimationFrame(h1ElAnim)
})
</script>

<template>
  <div class="whole-body">
    <div class="greeter-card">
      <h1 ref="h1El">Welcome, <Accented>User</Accented></h1>
      <p ref="pEl">Press Any Key To Continue</p>
    </div>
  </div>
</template>

<style scoped>
.whole-body {
  height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
}

.greeter-card {
  font-size: 2.5rem;
  width: 50vw;
  height: 30vh;
  text-align: center;
  display: flex;
  flex-direction: column;
  justify-content: space-evenly;
  background-color: hsla(204, 88%, 23%, 80%);
  padding: 2vh 5vw;
}

h1 {
  margin: 2vh auto;
  /* padding-right: 1ch; */
}

p {
  /* margin-top: 3vh; */
  /* margin-right: 2ch; */
  margin: 3vh auto 0 auto;  /* margin right will be set to 2ch by code for aesthetic purposes */
}

h1, p {
  overflow: hidden;
  white-space: nowrap;
  border-right: .7ch solid hsla(179, 88%, 46%, 0%);
  width: 0;
  animation: blinking-caret .5s linear infinite alternate;
  animation-play-state: paused;  /* will be set to running with code */
}

@keyframes blinking-caret {
  from {
    border-right-color: hsla(179, 88%, 46%, 0%);
  }
  to {
    border-right-color: hsla(179, 88%, 46%, 100%);
  }
}
</style>