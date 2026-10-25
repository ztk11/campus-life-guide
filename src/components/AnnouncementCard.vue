<script setup>
defineProps({ item: { type: Object, required: true } })
</script>

<template>
  <article class="announcement-card">
    <div class="announcement-meta"><span class="tag">{{ item.tag }}</span><time>{{ item.date }}</time></div>
    <h3>{{ item.title }}</h3><p>{{ item.text }}</p>
  </article>
</template>