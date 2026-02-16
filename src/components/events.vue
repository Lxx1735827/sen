<script setup>
const timeline = [
  {
    date: '2025.03.20',
    title: '初相识 💗',
    text: '这一天，我们的故事开始了'
  },
  {
    date: '2025.05.09',
    title: '我们在一起啦 💑',
    text: '终于正式在一起，心里甜甜的'
  },
  {
    date: '2025.06.28',
    title: '约会 🍷',
    text: '我们去了春熙路、玩了桌游、喝了小酒'
  },
  {
    date: '2025.07.09',
    title: '第一次逛博物馆 🏛️',
    text: '你看起来傻傻的很幼稚哈哈'
  },
  {
    date: '2025.07.29',
    title: '你的21岁 🎉',
    text: '也是我们的第一次深入交流'
  },
  {
    date: '2025.08.12',
    title: '第一次旅行 ✈️',
    text: '我们去了南京，我们是很合拍的旅游搭子！'
  },
  {
    date: '2025.10.18',
    title: '我的21岁 🎉',
    text: '“送君茉莉，愿君莫离”是你给我的礼物'
  },
  {
    date: '2025.10.24',
    title: '一起射箭 🏹',
    text: '享受和你在一起的每一秒'
  },
  {
    date: '2025.12.31',
    title: '跨年 🎆',
    text: '一起倒数，迎接新的一年，心里满是你'
  },
  {
    date: '2026.02.07',
    title: '拼豆 🐱',
    text: '世中逢尔，雨中逢花'
  } 
]
</script>

<template>
  <div class="timeline-container">
    <div class="timeline-line">
      <div v-for="(item, index) in timeline" :key="index" class="timeline-node">
        <div class="dot"></div>
        <div class="timeline-text">
          <div class="date">{{ item.date }}</div>
          <div class="title">{{ item.title }}</div>
          <p v-if="item.text">{{ item.text }}</p>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.timeline-container {
  width: 100%;
  overflow-x: auto;
  padding: 20px;
  -webkit-overflow-scrolling: touch; /* 手机滑动流畅 */

  /* 滚动条美化 */
  scrollbar-width: thin; /* Firefox */
  scrollbar-color: #f2b9c7 transparent;
}

/* Chrome / Edge / Safari */
.timeline-container::-webkit-scrollbar {
  height: 8px; /* 横向滚动条高度 */
}

.timeline-container::-webkit-scrollbar-track {
  background: transparent; /* 滑道透明 */
  border-radius: 4px;
}

.timeline-container::-webkit-scrollbar-thumb {
  background-color: #f2b9c7; /* 滑块颜色 */
  border-radius: 4px;
  border: 2px solid transparent;
  background-clip: content-box;
}

.timeline-container::-webkit-scrollbar-thumb:hover {
  background-color: #f2b9c7; /* 滑块悬浮时颜色更亮 */
}

/* 时间轴 */
.timeline-line {
  display: flex;
  align-items: flex-start;
  gap: 40px;
  min-width: max-content; /* 防止节点被压缩 */
  position: relative;
}

/* 节点 */
.timeline-node {
  display: flex;
  flex-direction: column;
  align-items: center;
  position: relative;
  flex-shrink: 0;
  min-width: 120px;
}

/* 横线连接 */
.timeline-node::after {
  content: '';
  position: absolute;
  top: 8px;
  left: 50%;
  width: 40px;
  height: 2px;
  background: #f5b6c8;
  transform: translateX(50%);
}

.timeline-node:last-child::after {
  display: none;
}

/* 节点圆点 */
.dot {
  width: 14px;
  height: 14px;
  border-radius: 50%;
  background: #f8b3c8;
  margin-bottom: 6px;
}

/* 节点文字 */
.timeline-text {
  text-align: center;
  max-width: 150px;
  font-size: 12px;
  color: #555;
}

.timeline-text .title {
  font-weight: bold;
  margin: 4px 0;
}

/* ===== 手机端适配 ===== */
@media (max-width: 768px) {
  .timeline-line {
    flex-direction: column;
    gap: 20px;
    min-width: unset;
  }

  .timeline-node {
    width: 90%;
  }

  .timeline-node::after {
    display: none; /* 手机竖向不画横线 */
  }
}
</style>
