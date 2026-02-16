<script setup>
import { ref, onMounted, onBeforeUnmount } from 'vue'

// 导入图片
import img1 from '/src/assets/img/1.jpg'
import img2 from '/src/assets/img/2.jpg'
import img3 from '/src/assets/img/3.jpg'

const images = [img1, img2, img3]
const currentIndex = ref(0)
let timer = null

// 自动轮播
const startAutoPlay = () => {
  stopAutoPlay()
  timer = setInterval(() => {
    currentIndex.value = (currentIndex.value + 1) % images.length
  }, 3000)
}

const stopAutoPlay = () => {
  if (timer) {
    clearInterval(timer)
    timer = null
  }
}

onMounted(startAutoPlay)
onBeforeUnmount(stopAutoPlay)

// 手动切换
const prev = () => {
  currentIndex.value =
    (currentIndex.value - 1 + images.length) % images.length
}

const next = () => {
  currentIndex.value = (currentIndex.value + 1) % images.length
}
</script>

<template>
  <div
    class="carousel"
    @mouseenter="stopAutoPlay"
    @mouseleave="startAutoPlay"
  >
    <div
      class="carousel-wrapper"
      :style="{ transform: `translateX(-${currentIndex * 100}%)` }"
    >
      <div
        class="carousel-item"
        v-for="(img, index) in images"
        :key="index"
      >
        <img :src="img" :alt="'Photo ' + (index + 1)" />
      </div>
    </div>

    <!-- 左右箭头 -->
    <button class="prev" @click="prev">‹</button>
    <button class="next" @click="next">›</button>
  </div>
</template>

<style scoped>
/* 轮播容器 */
.carousel {
  position: relative;
  width: 100%;
  max-width: 400px;
  aspect-ratio: 16 / 9;
  margin: 40px auto;
  overflow: hidden;
  border-radius: 14px;
  background-color: #000;
  box-shadow: 0 10px 20px rgba(0,0,0,0.2);
}

/* 轮播轨道 */
.carousel-wrapper {
  display: flex;
  width: 100%;
  height: 100%;
  transition: transform 0.5s ease;
}

/* 单张图 */
.carousel-item {
  flex: 0 0 100%;
  height: 100%;
}

.carousel-item img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  display: block;
}

/* 左右箭头（彻底去掉浏览器默认样式） */
.prev,
.next {
  position: absolute;
  top: 50%;
  transform: translateY(-50%);
  width: 36px;
  height: 36px;

  background: rgba(0,0,0,0.4);
  color: #fff;
  font-size: 22px;
  border-radius: 50%;
  cursor: pointer;
  z-index: 10;

  /* 🔥 关键：清除所有默认样式 */
  appearance: none;
  -webkit-appearance: none;
  -webkit-tap-highlight-color: transparent;
  border: none;
  outline: none;
  box-shadow: none;
  padding: 0;
}

.prev:hover,
.next:hover {
  background: rgba(0,0,0,0.65);
}

.prev { left: 10px; }
.next { right: 10px; }
</style>
