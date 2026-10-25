<script setup>
defineProps({ items: { type: Array, required: true } })
defineEmits(['remove'])
</script>

<template>
  <div v-if="items.length" class="favorite-list">
    <div v-for="item in items" :key="item.id" class="favorite-row">
      <span class="favorite-icon">{{ item.icon }}</span><div><strong>{{ item.name }}</strong><small>{{ item.category }} · {{ item.location }}</small></div>
      <button class="remove-button" @click="$emit('remove', item.id)" :aria-label="`取消收藏${item.name}`">×</button>
    </div>
  </div>
  <div v-else class="inline-empty">还没有收藏服务。可以先去校园服务页点亮爱心。</div>
</template>