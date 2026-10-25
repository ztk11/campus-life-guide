<script setup>
import { announcements, campusServices } from '../data/campus'
import WelcomeBanner from '../components/WelcomeBanner.vue'
import SectionHeading from '../components/SectionHeading.vue'
import StatCard from '../components/StatCard.vue'
import AnnouncementCard from '../components/AnnouncementCard.vue'
import ServiceCard from '../components/ServiceCard.vue'
import QuickLink from '../components/QuickLink.vue'

const featuredServices = campusServices.slice(0, 3)
</script>

<template>
  <div class="page-stack">
    <WelcomeBanner />
    <section class="stats-grid">
      <StatCard icon="▦" label="校园服务" :value="campusServices.length" note="持续整理" tone="blue" />
      <StatCard icon="✓" label="学习规划" value="随时" note="从小目标开始" tone="green" />
      <StatCard icon="♡" label="生活灵感" value="每日" note="发现新可能" tone="pink" />
    </section>
    <section>
      <SectionHeading title="常用校园服务" subtitle="常用入口整理在这里，快速找到需要的信息。" action-text="查看全部" action-to="/services" />
      <div class="service-grid">
        <ServiceCard v-for="service in featuredServices" :key="service.id" :service="service" @view-detail="$router.push('/services')" />
      </div>
    </section>
    <section class="home-bottom-grid">
      <div>
        <SectionHeading title="校园小提醒" subtitle="从日常小事开始，让校园生活更安心。" />
        <div class="announcement-list"><AnnouncementCard v-for="item in announcements" :key="item.id" :item="item" /></div>
      </div>
      <div>
        <SectionHeading title="快速开始" subtitle="选一个今天就能完成的小行动。" />
        <div class="quick-link-list">
          <QuickLink icon="▤" title="整理学习计划" description="添加一个学习小目标" to="/planner" tone="green" />
          <QuickLink icon="⌖" title="探索校园服务" description="查找常用地点与服务" to="/services" tone="purple" />
          <QuickLink icon="○" title="查看个人中心" description="回顾收藏与学习状态" to="/profile" tone="orange" />
        </div>
      </div>
    </section>
  </div>
</template>