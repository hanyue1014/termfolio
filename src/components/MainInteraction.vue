<script setup>
import Accented from './reusable/Accented.vue';</script>

<template>
<div class="vert-grid">
  <div class="output-container">
    <div class="output">
      <p style="font-size: 2em;">Welcome to Hanyue's <Accented>Termfolio</Accented> (terminal styled portfolio)</p>
      <p>Logged in as User@<Accented>skyhanyue</Accented></p>
      <p>Listening for commands...</p>
    </div>
  </div>
  <div class="input">
    <input type="text" placeholder="Type Command Here">
    <button>Run</button>
  </div>
</div>
</template>

<style scoped>
.vert-grid {
  display: grid;
  grid-template-rows: 9fr 1fr;
  row-gap: 3vh;
}

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

.input {
  display: flex;
  justify-content: center;
}

.input input {
  width: 85%;
  padding: 0px 2ch;
  font-size: 2em;
  font-family: 'Ubuntu Mono', monospace;
  border: none;
  border-radius: 25px 0 0 25px;
  background: var(--div-bg);
  color: var(--text-color);
}

/* imma ignore IE, apparently cannot use , to combine them else it wont work on chrome */
::placeholder {
  color: var(--text-color);
  opacity: 0.65;
}

::-webkit-input-placeholder {
  color: var(--text-color);
  opacity: 0.65;
}

::-moz-placeholder {
  color: var(--text-color);
  opacity: 0.65;
}

.input input:focus {
  outline: none;
}

.input button {
  width: 15%;
  background: var(--accent);
  font-size: 1.5em;
  font-family: 'Ubuntu Mono', monospace;
  border: none;
  border-radius: 0 25px 25px 0;
  transition: 0.5s;
}

.input button:active {
  opacity: 0.7;
}

.input button:focus {
  outline: none;
}
</style>