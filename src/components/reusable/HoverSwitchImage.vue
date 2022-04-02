<script setup>
import { onMounted, ref } from 'vue';

const props = defineProps(['ori', 'hidden'])

const src = ref(props.ori)
const tempSrc = ref(null)

const isAnimating = ref(false)

const img = ref(null)

onMounted(() => {
  // console.log(img.value)
  // make it 1:1
  img.value.style.height = img.value.clientWidth + 'px'
})

function animation() {
  isAnimating.value = true
  img.value.classList.add('fade-out')

  setTimeout(() => {
    isAnimating.value = false
    img.value.classList.remove('fade-out')
    src.value = tempSrc.value
  }, 300)
}

function showHidden() {
  if (!isAnimating.value) {
    animation()
  }
  // not directly editing src because it will directly change the src, instead, make it inside another ref and when the animation finishes playing, only change the src
  tempSrc.value = props.hidden
}

function hideHidden() {
  if (!isAnimating.value) {
    animation()
  }
  tempSrc.value = props.ori
}
</script>

<template>
<img :src="src" alt="Top Secret Picture of me" @mouseenter="showHidden" @mouseleave="hideHidden" ref="img">
</template>

<style scoped>
img {
  width: 100%;
  border-radius: 50%;
  transition: .3s;
}

.fade-out {
  opacity: 0;
}
</style>