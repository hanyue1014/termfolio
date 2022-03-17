<script setup>
import CommandBtn from './reusable/CommandBtn.vue';
</script>

<template>
<div class="commands">
  <h1>Commands</h1>
  <div class="command-btns">
    <CommandBtn btn-text="about" />
    <CommandBtn btn-text="contacts" />
    <CommandBtn btn-text="skills" />
    <CommandBtn btn-text="ls -R" />
  </div>
</div>
</template>

<style scoped>
.commands {
  padding: 5vh 2vw;
  border-radius: 25px;
  background: var(--div-bg);
}

h1 {
  text-align: center;
  font-size: 2.25em;
}

.command-btns {
  display: flex;
  flex-direction: column;
  margin-top: 45%;
}
</style>