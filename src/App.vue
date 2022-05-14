<script setup>
import { ref } from 'vue';
import Landing from './components/Landing.vue'
import Main from './components/Main.vue'

// save session storage, indicating user first time open this page
// naming can be quite confusing but this "firstTime" if user is first time here for the session, this wouldnt exist
let parsedURL = window.location.href.split('/')
// default user will be first time here
let firstTime = true
if (!window.sessionStorage.getItem('firstTime')) {
  // check if the url is legal as well, for now i don't have nested paths so when split '/', the length also shouldnt exceed 4
  // 0 for https/http, 1 for a empty string cuz thrs 2 /s, 2 for the hostname, 3 for the empty string cuz thrs a / behind the hostname as well, and if the user is indeed in some path, 3 will be the path
  // if the user came via an unvalid url, I want them to see the press to continue page as well
  if (parsedURL.length <= 4) {
    window.sessionStorage.setItem('firstTime', '1')
  }
} else {
  // if thr is indeed a 'firstTime' in session storage, this tab of user is not the first time here
  firstTime = false
}

// this will be abit hard to maintain but for now is ok as i quite certain it will only have 4 routes
let paths = ['about', 'contacts', 'skills', 'projects']

// in case future me staring at this code and questioning wtf am I doing
/**
 * i only want to show the press any key to continue page if and only if
 *   - the user is first time here
 *   - the user's route is legal and the path is one of my routes
 *   - so this logic is the interaction will be shown when this whole statement is true
 *   - if the path is one of my route, and is legal (less than length 4 (i do not have nested routes))
 *   - the reason i used OR is because i wanna make the condition true as long as parsedURL is invalid for my project
 *   - but this will only show IF the user is first time here AND there is no route in the path OR the path is invalid
 *   - lol imagine this took me 30 mins to come up with a logic like this
 */
let waitInteraction = ref(
  firstTime && (!paths.includes(parsedURL[3]) || parsedURL.length > 4)
)

function addListenerForNextPhase() {
  // directly let the window capture any interactions
  window.addEventListener('keypress', nextPhase)
  window.addEventListener('mousedown', nextPhase)
}

function nextPhase() {
  waitInteraction.value = !waitInteraction.value
  window.removeEventListener('mousedown', nextPhase)
  window.removeEventListener('keypress', nextPhase)
}
</script>

<template>
<Transition name="landing">
  <Landing v-if="waitInteraction" @add-listener="addListenerForNextPhase"/>
</Transition>
<Main :wait-interaction="waitInteraction"/>
</template>

<style>
@import url('https://fonts.googleapis.com/css2?family=Ubuntu+Mono&display=swap');

:root {
  --text-color: hsla(156, 100%, 90%, 100%);
  --accent: hsla(179, 88%, 46%, 100%);
  --div-bg: hsla(204, 88%, 23%, 100%);
  --bg-or-btn-text: hsla(246, 71%, 14%, 100%);
  --error: hsla(345, 63%, 49%, 100%);
}

* {
  margin: 0;
  padding: 0;
  transform-origin: center;
}

body {
  overflow: hidden;
}

#app {
  font-family: 'Ubuntu Mono', monospace;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  background: var(--bg-or-btn-text);
  color: var(--text-color);
  min-height: 100vh;
  margin: 0;
  padding: 0;
}

/* For the transition of the divs */
.landing-enter-active,
.landing-leave-active {
  transition: all 0.5s ease;
}

.landing-enter-from,
.landing-leave-to {
  transform: scale(1.5, 1.5);
  opacity: 0;
}

</style>
