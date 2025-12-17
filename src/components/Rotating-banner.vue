<template>
  <div class="rotating-contain">
    <div class="rotaing-back" :style="bgStyle"></div>
  </div>



</template>

<script setup>
import { ref, onMounted, onUnmounted, computed } from 'vue'

const images = [
  new URL('../assets/Character_art/千咲.jpg', import.meta.url).href,
  new URL('../assets/Character_art/仇远.jpg', import.meta.url).href,
  new URL('../assets/Character_art/嘉贝莉娜.jpg', import.meta.url).href,
  new URL('../assets/Character_art/奥古斯塔.jpg', import.meta.url).href,
  new URL('../assets/Character_art/尤诺.jpg', import.meta.url).href,
  new URL('../assets/Character_art/弗洛洛.jpg', import.meta.url).href,
  new URL('../assets/Character_art/琳奈立绘.jpg', import.meta.url).href,
]

const idx = ref(0)
let timer = null

const bgStyle = computed(() => ({
  backgroundImage: `url(${images[idx.value]})`,
  backgroundSize: 'cover',
  backgroundPosition: 'center',
  transition: 'background 0.6s ease'
}))

onMounted(() => {
  timer = setInterval(() => {
    idx.value = (idx.value + 1) % images.length
  }, 2000)
})

onUnmounted(() => {
  if (timer) clearInterval(timer)
})
</script>

<style scoped>
  .rotating-contain {
    position: relative;
    width: 100%;
    height: 500px;
    overflow: hidden;
  }
  .rotaing-back {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background-repeat: no-repeat;
    background-size: cover;
    background-position: center;
    will-change: background-image;
  }
</style>

