<script setup>
defineProps({
  eyebrow: { type: String, default: 'HELLO, CAMPUS' },
  title: { type: String, default: '把校园生活，安排得更有条理。' },
  description: { type: String, default: '校园服务、学习计划与日常提醒，一站式整理。' },
  actionText: { type: String, default: '探索校园服务' },
  actionTo: { type: String, default: '/services' }
})
</script>

<template>
  <section class="welcome-banner">
    <div class="banner-copy">
      <span class="eyebrow">{{ eyebrow }}</span>
      <h1>{{ title }}</h1>
      <p>{{ description }}</p>
      <RouterLink class="button button-light" :to="actionTo">{{ actionText }} <span>↗</span></RouterLink>
    </div>
    <div class="banner-art" aria-hidden="true">
      <div class="sun"></div><div class="art-book">✦</div>
      <div class="art-card card-one">📚<span>学习</span></div>
      <div class="art-card card-two">☕<span>生活</span></div>
      <div class="art-card card-three">✓<span>计划</span></div>
      <div class="art-plant">♧</div>
    </div>
  </section>
</template>