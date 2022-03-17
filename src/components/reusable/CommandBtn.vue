<script setup>
defineProps(['btnText'])
</script>

<template>

<button>{{ btnText }}</button>

</template>

<style scoped>
button {
  font-size: 1.75em;
  font-family: 'Ubuntu Mono', monospace;
  margin-bottom: 5vh;
  padding: 1.5vh 0;
  color: var(--bg-or-btn-text);
  background: var(--accent);
  border: none;
  border-radius: 10px;
  cursor: pointer;
  transition: box-shadow 0.5s, transform 0.3s;
}

button:hover {
  box-shadow: 0 3px 8px hsla(180, 100%, 88%, 100%);
  transform: translateY(-5px);
}

button:active {
    box-shadow: 0 2px 4px hsla(180, 100%, 88%, 100%);
    opacity: 0.8;
    transform: translateY(0);
}

button:focus {
  outline: none;
}
</style>