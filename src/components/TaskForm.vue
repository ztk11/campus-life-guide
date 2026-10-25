<script setup>
import { ref } from 'vue'
const emit = defineEmits(['add-task'])
const title = ref('')
const category = ref('课程学习')
const due = ref('')
function submitTask() {
  const cleanTitle = title.value.trim()
  if (!cleanTitle) return
  emit('add-task', { title: cleanTitle, category: category.value, due: due.value || '未设置' })
  title.value = ''
  due.value = ''
}
</script>

<template>
  <form class="task-form" @submit.prevent="submitTask">
    <label class="field-label">任务名称<input v-model="title" maxlength="60" placeholder="例如：复习 Python 列表与字典" required /></label>
    <div class="form-row">
      <label class="field-label">任务类型
        <select v-model="category"><option>课程学习</option><option>作业提交</option><option>个人成长</option><option>校园事务</option></select>
      </label>
      <label class="field-label">计划日期<input v-model="due" type="date" /></label>
    </div>
    <button class="button button-primary" type="submit">＋ 添加任务</button>
  </form>
</template>