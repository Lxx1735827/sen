<template>
  <div class="content-box">
    <span class="text">我们在一起的</span>

    <div class="calendar">
      <div class="calendar-page">
        <span class="number">{{ daysTogether }}</span>
      </div>
    </div>
    <span class="text">天</span>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue'

// 纪念日
const startDate = new Date('2025-05-09')

// 天数
const daysTogether = ref(0)

// 计算天数
const updateDays = () => {
  const today = new Date()
  const diffTime = today - startDate
  daysTogether.value = Math.floor(diffTime / (1000 * 60 * 60 * 24)) + 1
}

// 初始化
onMounted(() => {
  updateDays()
  
  // 每天更新一次
  setInterval(updateDays, 1000 * 60 * 60 * 24)
})
</script>

<style scoped>
.content-box {
  margin-top: 40px;
  display: flex;               
  align-items: center;         
  justify-content: center;     
  gap: 20px;                   
  color: #0a0a0a;
  font-family: "Helvetica", "Arial", sans-serif;
}

/* 文字样式 */
.text {
  font-size: 20px;
  font-weight: 500;
}

/* 日历容器 */
.calendar {
  width: 140px;
  height: 160px;
  perspective: 1000px;
}

/* 日历页 */
.calendar-page {
  width: 100%;
  height: 100%;
  background: #ffffff;
  color: #111;
  border-radius: 16px;

  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;

  box-shadow: 0 20px 40px rgba(0, 0, 0, 0.3);

  animation: flipIn 0.8s ease;
  transform-origin: top;
  transition: all 0.5s ease; /* 数字变化平滑 */
}

/* 数字 */
.number {
  font-size: 56px;
  font-weight: bold;
  line-height: 1;
}

/* 天字 */
.label {
  margin-top: 8px;
  font-size: 16px;
  opacity: 0.7;
}

/* 翻页动画 */
@keyframes flipIn {
  0% {
    transform: rotateX(-90deg);
    opacity: 0;
  }
  100% {
    transform: rotateX(0deg);
    opacity: 1;
  }
}
</style>
