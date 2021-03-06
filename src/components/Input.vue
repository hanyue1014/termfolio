<script setup>
import { ref } from 'vue';

const emit = defineEmits(['runCommand'])

const isFocus = ref(false)
const isPressed = ref(false)
const emptyError = ref(false)
const errorPopUp = ref(false)

const commandTyped = ref('')

function sendCommand() {
  if (!commandTyped.value) {
    // directly exit if the command typed is empty
    // alert('Please enter a command first')
    emptyError.value = true
    errorPopUp.value = true
    // close the pop up after 1s
    setTimeout(() => { errorPopUp.value = false }, 2000)
    return
  }

  emit('runCommand', commandTyped.value)
  commandTyped.value = ''
}

function inputChanged() {
  if (!!commandTyped.value) {
    // the user has typed smtg, remove the errorempty class
    emptyError.value = false
    errorPopUp.value = false  // if user inputted smtg, close the pop up early
  }
}

function simulatePress() {
  sendCommand()
  isPressed.value = true
  // cancel the value after like .2s
  setTimeout(() => { isPressed.value = false }, 200)
}
</script>

<template>
<div class="input" :class="{focus: (isFocus && !emptyError), pressed: (isPressed && !emptyError), error: emptyError, errorPopup: errorPopUp}">
  <!-- blur event fires when an element loses focus -->
  <input 
    type="text" 
    placeholder="Type Command Here"
    maxlength="30"
    v-model="commandTyped"
    @focus="() => isFocus = true" 
    @blur="() => isFocus = false" 
    @keyup.enter="simulatePress"
    @input="inputChanged">
  <button 
    @focus="() => isFocus = true" 
    @blur="() => isFocus = false" 
    @click="simulatePress"
  >Run</button>
</div>
</template>

<style scoped>
.input {
  display: flex;
  border-radius: 25px;  /* its children all 25px radius */
  justify-content: center;
  transition: .3s;
}

.focus {
  box-shadow: 0 3px 8px hsla(180, 100%, 88%, 100%);
  transform: translateY(-5px);
}

.pressed {
    box-shadow: 0 2px 4px hsla(180, 100%, 88%, 100%);
    transform: translateY(0);
}

.error {
  position: relative;
  box-shadow: 0 4px 4px var(--error);
}

.errorPopup::before {
  content: "Please type something";
  position: absolute;
  display: block;
  padding: 15px;
  font-size: 1.5em;
  left: 20%;
  background-color: var(--error);
  border-radius: 15px;
  animation: slide-in-from-btm .2s ease-in-out forwards;
}

@keyframes slide-in-from-btm {
  from {
    top: 0;
    opacity: 0;
  }

  to {
    top: -80%;
    opacity: 1;
  }
}

.input input {
  width: 85%;
  padding: 0px 25px;  /* border radius left is 25 px */
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
  border: 2px solid var(--accent);
  border-radius: 0 25px 25px 0;
  cursor: pointer;
  transition: 0.5s;
}

.input button:active {
  opacity: 0.7;
}

.input button:hover, button:focus {
  color: var(--accent);
  background: var(--div-bg);
}

.input button:focus {
  outline: none;
}
</style>