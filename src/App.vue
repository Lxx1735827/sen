<script setup>
  import TimeBar from './components/time.vue'
  import Pictures from './components/pictures.vue'
  import Heart from './components/heart.vue'
  import Events from './components/events.vue'
  import Buttons from './components/button.vue'
  import Letter from './components/letter.vue'
</script>

<template>
  <div class="bar">
    <h2 class="title">森宝的专属猫窝💗</h2>
  </div>

  <div class="content-row">
    <TimeBar />
    <Pictures />
  </div>
  <div>
    <Heart />
  </div>
  <div>
    <Events />
  </div>
  <div>
    <Buttons />
  </div>
  <div>
    <Letter />
  </div>
</template>

<style scoped>
.bar {
  position: fixed;
  top: 0;
  left: 0;  
  letter-spacing: 1px;
  height: 50px;
  width: 100%;
  background: rgba(255, 214, 232, 0.9);
  display: flex;
  align-items: center;
  justify-content: center;
  z-index: 100;
}

/* ===== 默认：PC 端 ===== */
.content-row {
  display: flex;
  align-items: flex-start;
  justify-content: space-between;
  width: 100%;
  margin-top: 70px;
  padding: 0 40px;
  box-sizing: border-box;
  gap: 20px;
}

.content-row > * {
  flex: 1;
  min-width: 300px;
}

/* ===== 📱 手机端适配 ===== */
@media (max-width: 768px) {
  .content-row {
    flex-direction: column;   /* ⬅️ 改成上下排列 */
    align-items: stretch;     /* 撑满宽度 */
    padding: 0 12px;          /* 手机左右留白 */
    gap: 16px;
  }

  .content-row > * {
    min-width: unset;
    width: 100%;
  }

  .bar {
    height: 48px;
  }

  .title {
    font-size: 16px;
  }
}

</style>
