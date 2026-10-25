# 校园生活指南 Campus Life Guide

一个面向 Vue 3 初学者的校园生活指南前端项目。网站包含首页、校园服务、学习规划、个人中心四个页面，使用 Vue Router 进行页面导航，数据采用本地模拟数据，不需要后端。

## 一、运行环境

- Node.js：建议安装当前仍受支持的 LTS 版本
- npm：随 Node.js 一起安装
- 编辑器：VS Code 或 Trae
- 浏览器：Chrome、Edge 等现代浏览器

## 二、如何运行（Windows 初学者）

1. 下载并解压 `campus-life-guide.zip`。
2. 进入解压后的 `campus-life-guide` 文件夹。
3. 在该文件夹空白处打开终端。VS Code / Trae 可通过“终端 → 新建终端”打开。
4. 输入 `node -v` 并回车。如果显示版本号，说明 Node.js 可用。
5. 输入 `npm -v` 并回车。如果显示版本号，说明 npm 可用。
6. 输入 `npm install` 并等待依赖安装完成。
7. 输入 `npm run dev`。
8. 终端会显示本地地址，通常类似 `http://localhost:5173/`。按住 Ctrl 点击链接，或复制到浏览器打开。
9. 修改代码后，Vite 通常会自动刷新页面。

如果提示 `node` 或 `npm` 不是命令，请先安装 Node.js LTS，然后关闭并重新打开终端。不要随意删除现有项目文件。

## 三、如何构建

在项目目录终端执行：

```bash
npm run build
```

成功后会生成 `dist` 文件夹。`dist` 是发布用的构建结果，不要手动修改其中的文件。

本地预览构建结果：

```bash
npm run preview
```

## 四、如何部署到 Netlify

1. 先在本地执行 `npm run build`，确认构建成功。
2. 将项目上传到 GitHub 仓库，或在 Netlify 中导入仓库。
3. Netlify 构建命令填写 `npm run build`。
4. 发布目录填写 `dist`。
5. 本项目已提供 `netlify.toml`，其中包含单页应用路由重定向配置。
6. 等待 Netlify 构建并显示部署成功，再复制平台生成的网址作为作业公网链接。

注意：项目文件本身并不等于已经部署。必须完成 Netlify 实际部署后，才能提交公网链接。

## 五、页面与组件

- `/` 首页：欢迎横幅、统计卡片、常用服务、公告、快捷入口
- `/services` 校园服务：关键词搜索、分类筛选、收藏、详情弹窗
- `/planner` 学习规划：添加任务、切换完成状态、删除任务、筛选任务、计算完成率
- `/profile` 个人中心：编辑昵称和专业、查看收藏服务

项目包含 22 个 `.vue` 单文件组件（包含根组件、4 个页面组件和可复用组件）。

## 六、关键代码逻辑

### 1. Vue 单文件组件（SFC）

`.vue` 文件通常由 `<script setup>`、`<template>` 和可选的 `<style>` 组成。本项目把样式集中放在 `src/assets/main.css`，方便初学者统一调整页面外观。

### 2. `ref`

`ref()` 用来创建响应式数据。例如 `ServicesView.vue` 的 `searchText` 保存搜索关键词。用户输入时数据变化，Vue 会自动更新相关页面。

### 3. `v-model`

`ServiceSearch.vue` 使用 `defineModel()` 与父组件建立双向绑定；`TaskForm.vue` 使用 `v-model` 读取表单输入。用户输入的内容会同步到响应式变量。

### 4. `v-for` 与 `:key`

列表组件使用 `v-for` 展示服务、任务和公告。`:key` 为每一项提供稳定标识，帮助 Vue 高效更新列表。

### 5. `v-if`

在搜索无结果、任务列表为空或弹窗关闭时，使用 `v-if` 控制内容是否显示。

### 6. 事件与 `defineEmits`

例如 `ServiceCard.vue` 发出 `toggle-favorite` 事件，父页面 `ServicesView.vue` 接收事件并更新收藏数组。子组件负责展示和发出事件，父组件负责管理数据。

### 7. `computed`

`ServicesView.vue` 用计算属性筛选服务；`PlannerView.vue` 用计算属性计算已完成任务数量、完成率与当前筛选列表。依赖数据变化时，计算结果自动更新。

### 8. Vue Router

`src/router/index.js` 定义四条路由。`RouterLink` 用于页面跳转，`RouterView` 用于显示当前路由对应的页面。

### 9. 动态属性与条件 class

`:class` 根据当前状态切换样式，例如已完成任务显示删除线；`:style` 将计算得到的百分比设置为进度条宽度。

### 10. 表单提交

`@submit.prevent` 会阻止浏览器默认刷新行为，再调用 JavaScript 函数处理任务新增或资料保存。

### 11. 生命周期

当前项目以响应式数据、计算属性和组件事件为主。若课堂要求展示生命周期，可在任意页面的 `<script setup>` 中加入以下示例，观察页面加载时控制台输出：

```js
import { onMounted, onUnmounted } from 'vue'

onMounted(() => {
  console.log('组件已挂载')
})

onUnmounted(() => {
  console.log('组件即将卸载')
})
```

## 七、建议的演示顺序

1. 首页展示布局与导航。
2. 进入“校园服务”，输入“图书馆”，演示搜索。
3. 切换分类，演示筛选。
4. 点击爱心，演示收藏状态。
5. 进入“学习规划”，添加任务、标记完成、删除任务。
6. 观察完成率随任务状态变化。
7. 进入“个人中心”，编辑昵称并保存。
8. 介绍组件拆分与父子组件通信。

## 八、可能被老师问到的问题

**问：为什么要拆分组件？**
答：把导航栏、服务卡片、任务项等独立出来，可以复用代码、减少重复，也更容易维护。

**问：`ref` 和 `computed` 有什么区别？**
答：`ref` 保存响应式状态；`computed` 根据已有状态计算出派生结果，例如任务完成率。

**问：父组件怎么把数据传给子组件？**
答：通过 `props` 传入，例如父组件把 `service` 对象传给 `ServiceCard`。

**问：子组件怎么通知父组件？**
答：通过 `defineEmits` 发出自定义事件，父组件监听事件后更新状态。

**问：为什么使用 Vue Router？**
答：它能根据 URL 显示不同页面，并支持页面间导航，而不需要为每个页面单独创建一套项目。

**问：数据刷新后为什么会恢复？**
答：本项目数据保存在内存中的响应式变量，没有接入数据库或浏览器持久化存储。若需要刷新后保留数据，可以继续学习 `localStorage`。

**问：这个网站是否连接学校真实数据？**
答：没有。当前是纯前端课程演示项目，地点、开放时间和任务均为模拟或本地状态数据。

## 九、Vue 官方教程对应知识点

- 模板语法与文本插值：标题、服务名、任务文本
- 属性绑定：`:class`、`:style`、`:aria-label`
- 事件处理：`@click`、`@submit`
- 响应式基础：`ref`
- 计算属性：`computed`
- 条件渲染：`v-if`
- 列表渲染：`v-for` 与 `:key`
- 表单输入绑定：`v-model`、`defineModel`
- 组件基础：多个 `.vue` 文件
- Props：`defineProps`
- 事件：`defineEmits`
- 组件组合：页面组合多个可复用组件
- 生命周期：README 中提供 `onMounted` / `onUnmounted` 演示
- 路由：Vue Router

## 十、提交前检查清单

- [ ] `npm install` 成功
- [ ] `npm run dev` 成功
- [ ] 四个页面均能打开
- [ ] 搜索与分类筛选正常
- [ ] 收藏、任务新增/完成/删除正常
- [ ] 个人资料编辑正常
- [ ] `npm run build` 成功
- [ ] 截取真实运行页面截图并放入实验报告
- [ ] 完成 Netlify 部署后再填写公网链接
