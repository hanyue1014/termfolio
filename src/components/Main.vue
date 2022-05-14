<script setup>
import { computed, ref } from 'vue';

import Header from './Header.vue'
import Commands from './Commands.vue';
import MainInteraction from './MainInteraction.vue';
import About from './Abouts.vue'
import Contacts from './Contacts.vue'

const props = defineProps(['waitInteraction'])  // here for the App.vue (if App.vue wants interaction, don't show any window prematurely)
const commands = ref([])

const routes = {
  '/': null,
  '/about': About,
  '/contacts': Contacts,
  '/skills': null,
  '/projects': null
}

const currentPath = ref('/' + window.location.href.split('/')[3])  // 0 is http 1 is empty (thr are 2 /s) 2 is the main page url

// only open the window if it is a valid path (for my use case, the path length will be 4 atmost, see App.vue for details)
if (window.location.href.split('/').length > 4) {
  currentPath.value = '/'
}

const windowOpened = computed(() => {
  if (!(routes[currentPath.value || '/'])) {
    // still, if it is undefined I would like to keep the url at root level just to be safe
    history.pushState(
      {},
      null,
      '/'
    )
    // reset the currentpath value as this computed depends on it to work
    currentPath.value = '/' + window.location.href.split('/')[3]
  }
  // safeguard in case the user went to some existed route but wanna show the user the "press to continue page"
  console.log(props.waitInteraction)
  return props.waitInteraction ? null : routes[currentPath.value || '/']
})

function changeLink(link) {
  history.pushState(
    {},
    null,
    link
  )
  currentPath.value = '/' + window.location.href.split('/')[3]
}

function sendToOutput(command) {
  commands.value.push(command)
  changeLink(command)
}

function closeWindow() {
  history.pushState(
    {},
    null,
    '/'
  )
  // for now i have to refresh the currentpath thing manually
  currentPath.value = '/' + window.location.href.split('/')[3]
}
</script>

<template>
<div class="container">
  <Header />
  <div  class="command-section-container">
    <MainInteraction :commands="commands" @run-command="sendToOutput" />
    <Commands @run-command="sendToOutput" />
  </div>
  <Transition name="window">
    <component :is="windowOpened" @close-window="closeWindow"></component>
  </Transition>
</div>
</template>

<style scoped>
.container {
  display: grid;
  grid-template-rows: 1fr 10fr;
  margin: 0 10vw;
  height: 100vh;
}

.command-section-container {
  display: grid;
  grid-template-columns: 7fr 3fr;
  margin: 2vh 0;
  gap: 3vw;
}

/* For the transition of the divs */
.window-enter-active,
.window-leave-active {
  transition: all 0.5s ease;
}

.window-enter-from,
.window-leave-to {
  opacity: 0;
}
</style>