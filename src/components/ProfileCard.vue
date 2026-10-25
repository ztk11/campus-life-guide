<script setup>
defineProps({
  nickname: { type: String, default: '校园探索者' },
  major: { type: String, default: '数据科学与大数据技术' },
  year: { type: String, default: '本科生' }
})
</script>

<template>
  <section class="profile-card">
    <div class="profile-cover"></div>
    <div class="profile-content"><div class="profile-avatar">同</div><span class="tag">CAMPUS MEMBER</span><h2>{{ nickname }}</h2><p>{{ major }}</p><div class="profile-divider"></div><div class="profile-info"><span>学习阶段</span><strong>{{ year }}</strong></div></div>
  </section>
</template>