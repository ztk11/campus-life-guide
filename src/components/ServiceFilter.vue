<script setup>
defineProps({ categories: { type: Array, required: true } })
const selected = defineModel({ type: String, default: '全部' })
</script>

<template>
  <div class="filter-row" aria-label="服务分类筛选">
    <button v-for="category in categories" :key="category" class="filter-chip" :class="{ selected: selected === category }" @click="selected = category">
      {{ category }}
    </button>
  </div>
</template>