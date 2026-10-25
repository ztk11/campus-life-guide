<script setup>
defineProps({
  completed: { type: Number, required: true },
  total: { type: Number, required: true },
  rate: { type: Number, required: true }
})
</script>

<template>
  <section class="progress-card">
    <div class="progress-head"><div><span class="eyebrow">YOUR PROGRESS</span><h3>一点点积累，也很了不起。</h3></div><strong>{{ rate }}%</strong></div>
    <div class="progress-track"><div class="progress-fill" :style="{ width: `${rate}%` }"></div></div>
    <p>已完成 {{ completed }} 项，共 {{ total }} 项任务。继续保持自己的节奏。</p>
  </section>
</template>