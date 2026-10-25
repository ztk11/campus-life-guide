<script setup>
defineProps({ task: { type: Object, required: true } })
defineEmits(['toggle', 'remove'])
</script>

<template>
  <article class="task-item" :class="{ completed: task.completed }">
    <button class="task-check" :aria-label="task.completed ? '标记未完成' : '标记完成'" @click="$emit('toggle', task.id)">{{ task.completed ? '✓' : '' }}</button>
    <div class="task-main"><strong>{{ task.title }}</strong><div class="task-meta"><span class="tag">{{ task.category }}</span><span>日期：{{ task.due }}</span></div></div>
    <button class="remove-button" @click="$emit('remove', task.id)" aria-label="删除任务">×</button>
  </article>
</template>