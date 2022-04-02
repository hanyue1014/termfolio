<script setup>
// README: there are still some logic error like it will animate non-stop if the user decided to leave for a while and hover back
// however i think it will be quite interesting as a feature (YEP Its not a bug its a feature)
import { ref } from 'vue';

const props = defineProps(['ori', 'hidden'])

const textDisplay = ref(props.ori)

const mouseHasLeft = ref(false)

function animateRemoveText(cback, param) {
  let remove_lastTime = null

  let removeText = time => {
    if (!remove_lastTime) {
      remove_lastTime = time
    }

    if (textDisplay.value.length > 0) {
      // i wan the words be removed .1s per word
      if ((time - remove_lastTime) / 1000 >= 0.1 ) {
        remove_lastTime = time
        textDisplay.value = textDisplay.value.slice(0, textDisplay.value.length - 1)
      }
      window.requestAnimationFrame(removeText)
    } else {
      // animation done, run the cback
      cback(param)
    }
  }

  window.requestAnimationFrame(removeText)
}

function animateAddText(changeTo) {
  let add_lastTime = null
  let length = 0

  let addText = time => {
    if (!add_lastTime) {
      add_lastTime = time
    }

    if (textDisplay.value.length < changeTo.length) {
      // i wan the words come out .1s per word
      if ((time - add_lastTime) / 1000 >= 0.1 ) {
        // need refresh the time else the code will always be runned becuz the time will always make the condition true
        add_lastTime = time
        textDisplay.value = changeTo.slice(0, length++)
      }
      window.requestAnimationFrame(addText)
    } else {
      if (mouseHasLeft.value && textDisplay.value === props.hidden) {
        // do check if the user mouse left in between and didnt comeback, change back to props.ori
        animateRemoveText(animateAddText, props.ori)
      } else if (!mouseHasLeft.value && textDisplay.value === props.ori) {
        // if the mouse is still in but the text is still ori, make the animation and make it back to hidden
        animateRemoveText(animateAddText, props.hidden)
      }
    }
  }

  window.requestAnimationFrame(addText)
}

function changeText() {
  mouseHasLeft.value = false
  animateRemoveText(animateAddText, props.hidden)
}

function mouseLeft() {
  mouseHasLeft.value = true
  // it is possible user's mouse has remained in the span, in that case, we just run removetext than add text agn to be sure 
  //(this can be tested by checking if the value of textDisplay is props.hidden)
  if (textDisplay.value === props.hidden) {
    animateRemoveText(animateAddText, props.ori)
  }
}
</script>

<template>
<div @mouseenter="changeText" @mouseleave="mouseLeft" >
  <span>{{ textDisplay }}</span>
</div>
</template>

<style scoped>
div {
  display: inline-block;
}

span {
  color: var(--accent);
  /* display: inline-block;  for width to work with span */
}
</style>