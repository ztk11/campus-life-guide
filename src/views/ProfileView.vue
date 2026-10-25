<script setup>
import { computed, ref } from 'vue'
import { campusServices } from '../data/campus'
import ProfileCard from '../components/ProfileCard.vue'
import SectionHeading from '../components/SectionHeading.vue'
import StatCard from '../components/StatCard.vue'
import FavoriteList from '../components/FavoriteList.vue'

const nickname = ref('校园探索者')
const major = ref('数据科学与大数据技术')
const editing = ref(false)
const draftName = ref(nickname.value)
const draftMajor = ref(major.value)
const favorites = ref([1, 3])
const favoriteServices = computed(() => campusServices.filter(service => favorites.value.includes(service.id)))
function saveProfile() {
  if (draftName.value.trim()) nickname.value = draftName.value.trim()
  if (draftMajor.value.trim()) major.value = draftMajor.value.trim()
  editing.value = false
}
function removeFavorite(id) {
  favorites.value = favorites.value.filter(item => item !== id)
}
</script>

<template>
  <div class="page-stack">
    <div class="page-intro"><span class="eyebrow">YOUR CAMPUS SPACE</span><h1>个人中心</h1><p>查看个人资料与收藏内容，打造更适合自己的校园工具箱。</p></div>
    <div class="profile-layout">
      <div class="profile-main">
        <ProfileCard :nickname="nickname" :major="major" />
        <section class="panel">
          <div class="section-heading"><div><h2>个人资料</h2><p>修改后会立即更新页面显示。</p></div><button class="text-button" @click="editing = !editing">{{ editing ? '取消编辑' : '编辑资料' }}</button></div>
          <form v-if="editing" class="task-form" @submit.prevent="saveProfile">
            <label class="field-label">昵称<input v-model="draftName" required maxlength="30" /></label>
            <label class="field-label">专业<input v-model="draftMajor" required maxlength="60" /></label>
            <button class="button button-primary" type="submit">保存修改</button>
          </form>
          <div v-else class="profile-info-list"><div><span>昵称</span><strong>{{ nickname }}</strong></div><div><span>专业方向</span><strong>{{ major }}</strong></div><div><span>学习阶段</span><strong>本科生</strong></div></div>
        </section>
      </div>
      <div class="profile-side">
        <div class="stats-grid profile-stats">
          <StatCard icon="♡" label="收藏服务" :value="favorites.length" note="常用入口" tone="pink" />
          <StatCard icon="✦" label="个人目标" value="持续中" note="每天进步一点" tone="purple" />
        </div>
        <section class="panel">
          <SectionHeading title="我的收藏" subtitle="方便下次快速找到常用服务。" />
          <FavoriteList :items="favoriteServices" @remove="removeFavorite" />
        </section>
        <div class="profile-tip"><span>✦</span><div><strong>给自己一点鼓励</strong><p>进步不一定每天都很明显，但持续行动会慢慢积累成果。</p></div></div>
      </div>
    </div>
  </div>
</template>