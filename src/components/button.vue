<script setup>
import { ref } from 'vue'

// 控制卡片显示
const showCard = ref(false)
const message = ref('')

// 情话/告白数组
const messages = [
  "别人问我最近在忙什么，我在忙着喜欢你",
  "日子普通又漫长，但只要有你，就刚刚好",
  "我偷偷把你放进我的心里，每天都想你",
  "我本来挺理性的，遇到你之后就开始胡思乱想了",
  "我不太会撒娇，但我会默默往你那边挪",
  "遇见便是上上签"
]

// 点击按钮随机选择一条
function toggleCard() {
  showCard.value = true
  const randomIndex = Math.floor(Math.random() * messages.length)
  message.value = messages[randomIndex]
}
</script>

<template>
  <div class="love-button-wrapper">
    <!-- 提示文字在爱心上方 -->
    <div class="button-text">点击几下，别笑，你也过不了第二关 😏</div>

    <!-- 爱心按钮 -->
    <button class="love-button" @click="toggleCard">
      ❤️
    </button>

    <!-- 弹出卡片 -->
    <transition name="fade-slide">
      <div v-if="showCard" class="love-card">
        <p>{{ message }}</p>
      </div>
    </transition>
  </div>
</template>

<style scoped>
.love-button-wrapper {
  display: flex;
  flex-direction: column;
  align-items: center;
  margin-top: 50px;
  position: relative;
}

/* 提示文字 */
.button-text {
  font-size: 16px;
  color: #ff5c8a;
  font-weight: bold;
  margin-bottom: 12px;
  text-align: center;
}

/* 爱心按钮 */
.love-button {
  background: #ff5c8a;
  border: none;
  border-radius: 50%;
  width: 100px;
  height: 100px;
  font-size: 40px;
  color: white;
  cursor: pointer;

  display: flex;             /* 使用 flex */
  align-items: center;       /* 垂直居中 */
  justify-content: center;   /* 水平居中 */
  line-height: 1;            /* 避免字体自带偏移 */
  transition: transform 0.2s;
}

.love-button:hover {
  transform: scale(1.2);
  box-shadow: 0 6px 14px rgba(255, 92, 138, 0.6);
}

/* 弹出卡片 */
.love-card {
  margin-top: 20px;
  background: #fff0f5;
  border: 2px solid #ff5c8a;
  border-radius: 16px;
  padding: 16px 20px;
  max-width: 280px;
  text-align: center;
  font-size: 14px;
  color: #ff5c8a;
  box-shadow: 0 8px 20px rgba(255, 92, 138, 0.3);
  position: relative;
}

/* 弹出动画 */
.fade-slide-enter-from {
  opacity: 0;
  transform: translateY(-10px);
}
.fade-slide-enter-to {
  opacity: 1;
  transform: translateY(0);
}
.fade-slide-leave-from {
  opacity: 1;
  transform: translateY(0);
}
.fade-slide-leave-to {
  opacity: 0;
  transform: translateY(-10px);
}
.fade-slide-enter-active,
.fade-slide-leave-active {
  transition: all 0.3s ease;
}
</style>
