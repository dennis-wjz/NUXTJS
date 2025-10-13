## 🧭 一、整体学习目标（总览）

学习目标是：

1. 掌握 Nuxt 的核心概念（SSR、路由、数据获取、插件、部署）
2. 能独立开发中小型 SSR 项目（如博客、CMS、后台管理、Shopify 前台等）
3. 能在现有 Vue3 项目中判断何时、为何使用 Nuxt

总周期建议：**4–6 周（每周 5~10 小时）**

------

## 📘 二、阶段学习计划

### **阶段一：Nuxt 核心入门（1 周）**

> 目标：理解 Nuxt 的整体架构、运行机制、目录结构与约定式开发。

#### 🔍 学习重点

- 什么是 Nuxt？SSR / SSG / CSR 的区别
- 目录结构（`pages`、`layouts`、`components`、`plugins`、`composables`、`server`）
- 路由系统（自动生成 + 动态路由）
- 使用 Pinia/VueUse 等 Vue 生态在 Nuxt 中的集成
- 基本布局与页面切换

#### 📚 推荐学习资料

- 官方文档：https://nuxt.com/docs
- 视频建议：Bilibili 搜索「Nuxt3 从入门到上线部署」或「Nuxt3 实战教程」
- 教程参考：
  - https://masteringnuxt.com/
  - https://nuxt.new （在线新建模板）

#### 💡 小练习

1. 创建一个最简单的博客骨架项目：

   ```
   npx nuxi init nuxt-blog
   cd nuxt-blog && npm install && npm run dev
   ```

2. 使用 `pages/` 自动生成路由；

3. 添加 `layouts/default.vue`，实现公共头部/底部。

------

### **阶段二：核心功能与服务端逻辑（2 周）**

> 目标：掌握 Nuxt 的核心运行机制和数据获取方式，能与后端交互。

#### 🔍 学习重点

- 服务端数据获取（`useAsyncData`、`useFetch`）
- 运行时配置（`useRuntimeConfig`）
- 插件系统（`plugins/axios.ts`、`plugins/i18n.ts`）
- 中间件（`middleware/auth.ts`）
- 服务端 API 路由（`server/api/`）
- SEO 与 meta 管理（`useHead`、`definePageMeta`）
- 静态资源与环境变量

#### 📚 推荐资源

- 官方数据获取章节：https://nuxt.com/docs/getting-started/data-fetching
- 掘金/B站搜索：「Nuxt3 + Axios 实战」、「Nuxt3 SEO」

#### 💡 小练习

构建一个「博客系统」原型：

- 首页：获取文章列表（模拟接口或本地 JSON）
- 详情页：动态路由 `/posts/[id].vue`
- 全局加载动画（中间件 + composable 控制）
- SEO：动态设置每篇文章的 title 与 description

------

### **阶段三：综合实战（2–3 周）**

> 目标：完成一个中小型项目，涵盖服务端渲染、接口交互、部署与性能优化。

#### 🧱 推荐项目方向（任选其一或组合）

| 实战项目                               | 主要练习点                             |
| -------------------------------------- | -------------------------------------- |
| **Nuxt + Supabase 博客系统**           | SSR、Auth、数据库、SEO、i18n           |
| **电商前台（Shopify 接口或模拟数据）** | 动态页面、分页、API 调用、缓存         |
| **后台管理系统（SSR + API mock）**     | 权限中间件、动态菜单、Pinia 状态持久化 |
| **个人主页/作品集网站**                | SEO + 动态数据 + 部署到 Vercel         |

#### 🧩 高级学习方向

- 部署：Vercel / Netlify / Cloudflare Pages
- API 层：使用 `server/api` 构建后端接口
- 国际化（`nuxt-i18n`）
- 性能优化（懒加载组件、预渲染）
- 集成 UI 框架（Element Plus / Naive UI / Tailwind）

#### 💡 最终挑战

做一个「多语言博客 + 管理后台」：

- 前台使用 Nuxt3 渲染博客内容（含 SEO）；
- 后台用 Element Plus（或 Naive UI）；
- 使用同一个 API 服务层（`server/api`）。

------

## 🧠 四、学习策略建议

- **每天 1~2 小时**，以「边做边学」为主；
- 优先看 **官方文档 + 官方模板**；
- 每个阶段完成一个 demo 就 push 到 GitHub；
- 笔记建议：每周总结「踩坑 + 新概念 + 收获」；
- 如果你擅长 Vue3 Composition API，可以多关注 `useAsyncData` 与 `composables` 的设计模式。

------

## 🧱 五、可以帮你搭的实战模板（任选）

我可以帮你定制：

1. ✅ Nuxt3 + Element Plus SSR 管理后台模板
2. ✅ Nuxt3 + Supabase 博客项目
3. ✅ Nuxt3 + Shopify API 前台展示
4. ✅ Nuxt3 + i18n + Pinia 多语言网站





