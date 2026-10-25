<script setup>
defineProps({
  icon: { type: String, required: true },
  title: { type: String, required: true },
  description: { type: String, required: true },
  to: { type: String, required: true },
  tone: { type: String, default: 'blue' }
})
</script>

<template>
  <RouterLink class="quick-link" :to="to">
    <span class="quick-icon" :class="tone">{{ icon }}</span>
    <span class="quick-copy"><strong>{{ title }}</strong><small>{{ description }}</small></span>
    <span class="quick-arrow">↗</span>
  </RouterLink>
</template>