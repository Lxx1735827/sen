<script setup>
import { ref, onMounted, onUnmounted } from 'vue'

const hearts = ref([])
let timer = null

function createHeart() {
  hearts.value.push({
    id: Date.now() + Math.random(),
    left: Math.random() * 100,          // 随机横向位置 %
    size: 12 + Math.random() * 20,      // 大小
    duration: 6 + Math.random() * 4     // 上浮时间
  })

  // 控制数量，避免太多
  if (hearts.value.length > 30) {
    hearts.value.shift()
  }
}

onMounted(() => {
  timer = setInterval(createHeart, 500)
})

onUnmounted(() => {
  clearInterval(timer)
})
</script>

<template>
  <div class="heart-container">
    <span
      v-for="heart in hearts"
      :key="heart.id"
      class="heart"
      :style="{
        left: heart.left + '%',
        fontSize: heart.size + 'px',
        animationDuration: heart.duration + 's'
      }"
    >
      💗
    </span>
  </div>
</template>

<style scoped>
.heart-container {
  position: fixed;
  inset: 0;
  pointer-events: none; /* 不挡点击 */
  overflow: hidden;
  z-index: 0;
}

.heart {
  position: absolute;
  bottom: -30px;
  animation: floatUp linear forwards;
  opacity: 0.8;
}

@keyframes floatUp {
  0% {
    transform: translateY(0) scale(1);
    opacity: 0.9;
  }
  100% {
    transform: translateY(-110vh) scale(1.4);
    opacity: 0;
  }
}
</style>
