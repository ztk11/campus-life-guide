<script setup>
const model = defineModel({ type: String, default: '' })
</script>

<template>
  <label class="search-box">
    <span>⌕</span>
    <input v-model="model" type="search" placeholder="搜索校园服务，例如：图书馆" aria-label="搜索校园服务" />
    <kbd>搜索</kbd>
  </label>
</template>