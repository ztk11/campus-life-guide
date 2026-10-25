<script setup>
import { computed, ref } from 'vue'
import { campusServices } from '../data/campus'
import SectionHeading from '../components/SectionHeading.vue'
import ServiceSearch from '../components/ServiceSearch.vue'
import ServiceFilter from '../components/ServiceFilter.vue'
import ServiceCard from '../components/ServiceCard.vue'
import EmptyState from '../components/EmptyState.vue'

const searchText = ref('')
const selectedCategory = ref('全部')
const favorites = ref([])
const activeService = ref(null)
const categories = ['全部', ...new Set(campusServices.map(item => item.category))]
const filteredServices = computed(() => {
  const keyword = searchText.value.trim().toLowerCase()
  return campusServices.filter(service => {
    const matchesCategory = selectedCategory.value === '全部' || service.category === selectedCategory.value
    const matchesSearch = !keyword || `${service.name} ${service.category} ${service.location} ${service.description}`.toLowerCase().includes(keyword)
    return matchesCategory && matchesSearch
  })
})
function toggleFavorite(id) {
  favorites.value = favorites.value.includes(id)
    ? favorites.value.filter(item => item !== id)
    : [...favorites.value, id]
}
</script>

<template>
  <div class="page-stack">
    <div class="page-intro"><span class="eyebrow">CAMPUS DIRECTORY</span><h1>校园服务</h1><p>把常用地点与生活服务整理在一起，搜索、筛选，快速找到方向。</p></div>
    <div class="service-toolbar"><ServiceSearch v-model="searchText" /><span class="result-count">找到 <strong>{{ filteredServices.length }}</strong> 项服务</span></div>
    <ServiceFilter v-model="selectedCategory" :categories="categories" />
    <div v-if="filteredServices.length" class="service-grid service-grid-large">
      <ServiceCard v-for="service in filteredServices" :key="service.id" :service="service" :favorite="favorites.includes(service.id)" @toggle-favorite="toggleFavorite" @view-detail="activeService = $event" />
    </div>
    <EmptyState v-else title="没有找到相关服务" description="请尝试其他关键词，或选择“全部”分类。" />
    <div v-if="activeService" class="modal-backdrop" @click.self="activeService = null" @keydown.esc="activeService = null">
      <section class="detail-modal" role="dialog" aria-modal="true" :aria-label="activeService.name + '详情'">
        <button class="modal-close" @click="activeService = null" aria-label="关闭">×</button>
        <div class="service-icon modal-icon" :class="activeService.color">{{ activeService.icon }}</div>
        <span class="service-category">{{ activeService.category }}</span><h2>{{ activeService.name }}</h2>
        <p>{{ activeService.description }}</p>
        <div class="detail-line"><span>地点</span><strong>{{ activeService.location }}</strong></div>
        <div class="detail-line"><span>开放时间</span><strong>{{ activeService.hours }}</strong></div>
        <p class="notice">提示：本网站为课程演示项目，地点与时间为示例信息，请以学校官方通知为准。</p>
        <button class="button button-primary full-button" @click="toggleFavorite(activeService.id)">{{ favorites.includes(activeService.id) ? '♥ 已收藏' : '♡ 收藏服务' }}</button>
      </section>
    </div>
    <div class="notice-strip">温馨提示：本页数据仅用于前端功能演示，实际地点、开放时间及办事要求请以学校官方信息为准。</div>
  </div>
</template>