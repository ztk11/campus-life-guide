<script setup>
defineProps({
  title: { type: String, required: true },
  subtitle: { type: String, default: '' },
  actionText: { type: String, default: '' },
  actionTo: { type: String, default: '/' }
})
</script>

<template>
  <div class="section-heading">
    <div><h2>{{ title }}</h2><p v-if="subtitle">{{ subtitle }}</p></div>
    <RouterLink v-if="actionText" class="text-link" :to="actionTo">{{ actionText }} ↗</RouterLink>
  </div>
</template>