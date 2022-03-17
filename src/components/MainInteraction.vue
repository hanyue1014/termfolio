<script setup></script>

<template>
<div class="vert-grid">
  <div class="output"></div>
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

.output{
  background-color: var(--div-bg);
  border-radius: 25px;
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
}

::-webkit-input-placeholder {
  color: var(--text-color);
}

::-moz-placeholder {
  color: var(--text-color);
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
}

.input button:focus {
  outline: none;
}
</style>