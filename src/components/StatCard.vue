<script setup>
defineProps({
  icon: { type: String, default: '✦' },
  label: { type: String, required: true },
  value: { type: [String, Number], required: true },
  note: { type: String, default: '' },
  tone: { type: String, default: 'blue' }
})
</script>

<template>
  <article class="stat-card">
    <div class="stat-top"><span class="stat-icon" :class="tone">{{ icon }}</span><span class="stat-note">{{ note }}</span></div>
    <strong class="stat-value">{{ value }}</strong>
    <span class="stat-label">{{ label }}</span>
  </article>
</template>