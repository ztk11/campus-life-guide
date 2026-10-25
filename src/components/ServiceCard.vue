<script setup>
defineProps({ service: { type: Object, required: true }, favorite: { type: Boolean, default: false } })
defineEmits(['toggle-favorite', 'view-detail'])
</script>

<template>
  <article class="service-card">
    <div class="service-card-top">
      <div class="service-icon" :class="service.color">{{ service.icon }}</div>
      <button class="icon-button" :aria-label="favorite ? '取消收藏' : '收藏服务'" @click="$emit('toggle-favorite', service.id)">
        {{ favorite ? '♥' : '♡' }}
      </button>
    </div>
    <span class="service-category">{{ service.category }}</span>
    <h3>{{ service.name }}</h3>
    <p>{{ service.description }}</p>
    <div class="service-meta"><span>⌖ {{ service.location }}</span><span>◷ {{ service.hours }}</span></div>
    <button class="card-link" @click="$emit('view-detail', service)">查看服务详情 <span>→</span></button>
  </article>
</template>