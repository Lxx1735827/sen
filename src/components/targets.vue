<script setup>
import { ref, computed } from 'vue'

// 定义 localStorage 的唯一标识（方便读取/保存，可自定义）
const STORAGE_KEY = 'couple_100_tasks'

// 【修改1：初始化时从 localStorage 读取数据，无则使用默认数组】
const initTasks = () => {
  // 从 localStorage 读取保存的字符串
  const savedTasks = localStorage.getItem(STORAGE_KEY)
  if (savedTasks) {
    // 还原为数组对象并返回
    try {
      return JSON.parse(savedTasks)
    } catch (e) {
      // 容错：如果数据格式损坏，返回默认数组
      console.error('读取本地任务数据失败，使用默认数据', e)
    }
  }
  // 默认示例清单
  return [
    { id: 1, text: '一起看一次日出 🌅', done: false },
    { id: 2, text: '去海边踩沙子 🏖️', done: false },
    { id: 3, text: '一起做饭 🍳', done: false },
    { id: 4, text: '一起看电影 🎬', done: false },
    { id: 5, text: '手牵手散步 🌙', done: false },
    { id: 6, text: '拍一张我们的合照 📸', done: false },
    { id: 7, text: '一起买情侣手链 💍', done: false },
    { id: 8, text: '一起做一件手工 🎨', done: false },
  ]
}

// 初始化响应式任务列表
const tasks = ref(initTasks())

// 统计完成数量
const completedCount = computed(() => tasks.value.filter(t => t.done).length)

// 【封装：保存任务数据到 localStorage（复用性更强）】
const saveTasksToStorage = () => {
  localStorage.setItem(STORAGE_KEY, JSON.stringify(tasks.value))
}

// 【修改2：切换状态后，同步保存到 localStorage】
function toggleTask(id) {
  const task = tasks.value.find(t => t.id === id)
  if (task) {
    task.done = !task.done
    // 数据更新后，立即保存到本地
    saveTasksToStorage()
  }
}
</script>

<template>
  <div class="checklist-container">
    <h3>我们的 100 件事 ✅</h3>
    <p>已完成 {{ completedCount }} / {{ tasks.length }}</p>

    <ul class="task-list">
      <li v-for="task in tasks" :key="task.id" :class="{ done: task.done }" @click="toggleTask(task.id)">
        <input type="checkbox" v-model="task.done" />
        <span>{{ task.text }}</span>
      </li>
    </ul>
  </div>
</template>

<style scoped>
.checklist-container {
  max-width: 700px;
  margin: 40px auto;
  padding: 20px;
  background: #fff0f5;
  border-radius: 16px;
  box-shadow: 0 6px 20px rgba(255, 92, 138, 0.2);
  color: #ff5c8a;
}

h3 {
  text-align: center;
  margin-bottom: 10px;
}

p {
  text-align: center;
  margin-bottom: 20px;
}

.task-list {
  list-style: none;
  padding: 0;
  display: grid;
  grid-template-columns: repeat(2, 1fr); /* 两列布局 */
  gap: 12px; /* 每个任务间距 */
}

.task-list li {
  display: flex;
  align-items: center;
  padding: 8px 12px;
  border-radius: 12px;
  cursor: pointer;
  background: #ffe6f0;
  transition: background 0.2s;
}

.task-list li:hover {
  background: #ffd1e6;
}

.task-list li.done {
  text-decoration: line-through;
  color: #aaa;
}

.task-list li input[type="checkbox"] {
  margin-right: 10px;
}

/* ===== 手机端适配 ===== */
@media (max-width: 768px) {
  .task-list {
    grid-template-columns: 1fr; /* 手机端一列显示 */
  }
}
</style>