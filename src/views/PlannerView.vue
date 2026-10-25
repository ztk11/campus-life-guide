<script setup>
import { computed, ref } from 'vue'
import SectionHeading from '../components/SectionHeading.vue'
import TaskForm from '../components/TaskForm.vue'
import TaskList from '../components/TaskList.vue'
import ProgressCard from '../components/ProgressCard.vue'
import EmptyState from '../components/EmptyState.vue'

let nextId = 4
const tasks = ref([
  { id: 1, title: '复习 Vue 模板语法与事件绑定', category: '课程学习', due: '本周', completed: true },
  { id: 2, title: '整理本周 Python 实验笔记', category: '作业提交', due: '本周', completed: false },
  { id: 3, title: '预习计算机专业英语词汇', category: '个人成长', due: '未设置', completed: false }
])
const activeFilter = ref('全部')
const filters = ['全部', '待完成', '已完成']
const completedCount = computed(() => tasks.value.filter(task => task.completed).length)
const completionRate = computed(() => tasks.value.length ? Math.round(completedCount.value / tasks.value.length * 100) : 0)
const visibleTasks = computed(() => tasks.value.filter(task => {
  if (activeFilter.value === '待完成') return !task.completed
  if (activeFilter.value === '已完成') return task.completed
  return true
}))
function addTask(payload) {
  tasks.value.unshift({ id: nextId++, ...payload, completed: false })
}
function toggleTask(id) {
  const task = tasks.value.find(item => item.id === id)
  if (task) task.completed = !task.completed
}
function removeTask(id) {
  tasks.value = tasks.value.filter(task => task.id !== id)
}
</script>

<template>
  <div class="page-stack">
    <div class="page-intro"><span class="eyebrow">SMALL STEPS, BIG PROGRESS</span><h1>学习规划</h1><p>不必一次完成所有事情，把目标拆小，按自己的节奏前进。</p></div>
    <ProgressCard :completed="completedCount" :total="tasks.length" :rate="completionRate" />
    <div class="planner-layout">
      <section class="panel">
        <SectionHeading title="添加新任务" subtitle="写下一个清晰、可执行的小目标。" />
        <TaskForm @add-task="addTask" />
      </section>
      <section class="panel task-panel">
        <SectionHeading title="我的任务" subtitle="点击圆圈切换完成状态。" />
        <div class="filter-row task-filters"><button v-for="filter in filters" :key="filter" class="filter-chip" :class="{ selected: activeFilter === filter }" @click="activeFilter = filter">{{ filter }}</button></div>
        <TaskList :tasks="visibleTasks" @toggle="toggleTask" @remove="removeTask" />
        <p class="tiny-note">任务数据保存在当前页面运行状态中；刷新页面后会恢复示例数据。</p>
      </section>
    </div>
    <EmptyState v-if="tasks.length === 0" icon="✦" title="新的开始" description="添加第一项任务，建立属于自己的学习节奏。" />
  </div>
</template>