<script setup>
import { ref } from 'vue'

// 你要显示的大段文本
const content = ref(`
亲爱的森宝 💗
新年快乐呀 🎆
不知不觉，我们已经在一起这么久了。
在过去的这段时光中，我们有欢声笑语，也有温柔相伴，所幸与你同行，岁月美好。
我们也产生过一些小磨合，或许就像健身一样，是为了一段坚固的关系，希望森宝不要因为这些对我产生隔阂。
感谢森宝能包容我，理解我。
我也会努力经营这一段关系，把你当成一只小猫咪。
祝森宝在新的一年天天开心，学业有成！
祝我们年年岁岁花相似，岁岁年年人相同。
爱你的渲宝 💗

`)
</script>

<template>
  <div class="text-container">
    <p>{{ content }}</p>
  </div>
</template>

<style scoped>
.text-container {
  max-width: 600px;          /* 最大宽度，太长不舒服 */
  margin: 40px auto;         /* 居中显示 */
  padding: 20px;             /* 内边距，文字不贴边 */
  background: #fff0f5;       /* 淡粉背景，温馨 */
  border-radius: 16px;       /* 圆角 */
  box-shadow: 0 6px 20px rgba(255, 92, 138, 0.2); /* 投影 */
  color: #ec85a2;            /* 文字颜色 */
  font-size: 16px;            /* 文字大小 */
  line-height: 1.8;          /* 行间距 */
  white-space: pre-wrap;     /* 保留换行符 */
  word-break: break-word;     /* 防止长单词撑破布局 */
}
</style>
