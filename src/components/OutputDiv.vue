<script setup>
import Accented from './reusable/Accented.vue';
import InfoOutput from './reusable/InfoOutput.vue';

defineProps(['commands'])

function scrollToBottom() {
  const container = document.querySelector("#to-be-scrolled")
  container.scrollTop = container.scrollHeight
}
</script>

<template>
<div class="output-container">
  <div class="output" id="to-be-scrolled">
    <p style="font-size: 2em;">Welcome to Hanyue's <Accented>Termfolio</Accented> (terminal styled portfolio)</p>
    <p>Logged in as User@<Accented>skyhanyue</Accented></p>
    <p>Listening for commands...</p>
    <InfoOutput
      v-for="command in commands"
      :commandToRun="command"
      @scroll-down="scrollToBottom" />
    <p>$ <span class="blinking-cursor">0</span></p>
  </div>
</div>
</template>

<style scoped>
.output-container {
  display: flex;
  align-items: center;
  background-color: var(--div-bg);
  border-radius: 25px;
  padding: 2vh 2vw;
}

.output {
  overflow-y: auto;
  height: 68vh;
  /* padding-right: 1vw; */
  width: 100%;
}

.output p {
  font-size: 1.5em;
  margin-top: 1vh;
}

.blinking-cursor {
  width: 1ch;
  color: var(--accent);  /* to hide the text inside the span element */
  background-color: var(--accent);
  animation: blinking-caret .5s linear infinite alternate;
  /* make the 0 not selectable as to further hide it */
  -webkit-touch-callout: none;
  -webkit-user-select: none;
  -khtml-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
}

@keyframes blinking-caret {
  from {
    opacity: 0;
  }
  to {
    opacity: 1;
  }
}
</style>