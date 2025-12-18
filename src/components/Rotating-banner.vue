<template>
  <!-- 轮播图部分 -->
  <div class="rotating-contain">
    <div class="back-contain" :style="bgStyle">
    <div class="figture-contain">
      <div class="button-figure">
         <button v-for="(img, i) in images" :key="i" :style="{ background: buttonbackcolor[currentColorIndex] }" :class="{ active: idx === i }" @click="setIdx(i)">{{ imagesfigure[i] }}</button>
      </div>
      <div class="rotaing-figure">
         <img :src="images[idx]" alt="figure" />
      </div>
    </div>
    </div>
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
const imagesfigure = [
  "千咲",
  "仇远",
  "嘉贝莉娜",
  "奥古斯塔",
  "尤诺",
  "弗洛洛",
  "琳奈"
]
const buttonbackcolor = [
  "rgba(219,138,118,0.425)",
  "rgba(128,181,63,0.425)",
  "rgba(40, 89, 161, 0.425)",
  "rgba(245,211,100,0.425)",
  "rgba(40, 89, 161, 0.425)",
  "rgba(219,138,118,0.425)",
  "rgba(231, 224, 224, 0.425)"
]
const idx = ref(0)
let timer = null
const currentColorIndex = computed(() => (idx.value  + images.length) % images.length)
function setIdx(i) {
  idx.value = i
}

const bgStyle = computed(() => ({
  backgroundImage: `url(${images[idx.value]})`,
  backgroundSize: 'cover',
  backgroundPosition: 'bottom',
  transition: 'background 0.4s ease'
}))

onMounted(() => {
  timer = setInterval(() => {
    idx.value = (idx.value + 1) % images.length
  }, 5000)
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

  /* 轮播图背景样式 */
  .back-contain {
    position: relative;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    border-radius: 30px;
    background-repeat: no-repeat;
    background-size: cover;
    background-position: center;
  }

  /* 轮播图立绘样式 */
  .figture-contain{
    position: absolute;
    width: 45%;
    height: 100%;
    top: 0;
    left: 50%;
    transform: translateX(-50%);
    z-index:1;
    display: flex;
    
  }
  /* 按钮样式 */
  .button-figure {
    width: 33%;
    height: 100%;
    flex-direction: column;
    display: flex;
    border-radius: 15px;
    justify-content: space-between;
    z-index: 2;
  }
  .button-figure button{
    border: none;
    flex: 1;
    padding: 6px 10px;
    font-size: 30px;
    border-radius: 15px;
  }
  .button-figure button.active{
    box-shadow: 0 0 12px 12px rgba(45, 44, 44, 0.08) inset;
    flex: 2;
    font-size: 40px;
    color: white;
  }
  /* 轮播图 人物样式 */
  .rotaing-figure {
    position: relative;
    top: -20%;
    width: 66%;
    z-index: 2;
    align-items: flex-end;
    /* 底部对齐 */
    pointer-events: none;
  }
  .rotaing-figure img{
    width: 100%;
    height: auto;
  }
</style>

