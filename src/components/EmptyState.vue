<script setup>
defineProps({
  icon: { type: String, default: '⌕' },
  title: { type: String, default: '暂时没有内容' },
  description: { type: String, default: '试试调整筛选条件吧。' }
})
</script>

<template>
  <div class="empty-state"><span>{{ icon }}</span><h3>{{ title }}</h3><p>{{ description }}</p></div>
</template>