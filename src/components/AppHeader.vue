<script setup>
import { useRoute } from 'vue-router'
const route = useRoute()
const links = [
  { to: '/', label: '首页', icon: '⌂' },
  { to: '/services', label: '校园服务', icon: '▦' },
  { to: '/planner', label: '学习规划', icon: '✓' },
  { to: '/profile', label: '个人中心', icon: '○' }
]
</script>

<template>
  <header class="topbar">
    <RouterLink to="/" class="brand">
      <span class="brand-mark">C</span>
      <span><strong>校园生活指南</strong><small>Campus Life Guide</small></span>
    </RouterLink>
    <nav class="main-nav" aria-label="主导航">
      <RouterLink v-for="link in links" :key="link.to" :to="link.to" :class="{ active: route.path === link.to }">
        <span class="nav-icon">{{ link.icon }}</span>{{ link.label }}
      </RouterLink>
    </nav>
    <RouterLink to="/profile" class="avatar-link" aria-label="个人中心">同</RouterLink>
  </header>
</template>