<script setup>
import TaskItem from './TaskItem.vue'
defineProps({ tasks: { type: Array, required: true } })
defineEmits(['toggle', 'remove'])
</script>

<template>
  <div v-if="tasks.length" class="task-list">
    <TaskItem v-for="task in tasks" :key="task.id" :task="task" @toggle="$emit('toggle', $event)" @remove="$emit('remove', $event)" />
  </div>
  <div v-else class="inline-empty">当前筛选下没有任务，试着添加一个小目标。</div>
</template>