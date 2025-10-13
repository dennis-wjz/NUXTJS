# 🥇 项目一：Nuxt3 + Element Plus SSR 管理后台模板

## 🎯 目标

实现一套可复用的 SSR 管理后台模板，包含登录、权限控制、动态菜单。

------

## 🧩 技术栈

- Nuxt3
- Element Plus
- Pinia
- Axios (通过插件封装)
- SSR + RESTful API

------

## ⚙️ 安装命令

```
npx nuxi init nuxt-admin
cd nuxt-admin
npm install element-plus axios pinia
npm run dev
```

------

## 📁 目录结构

```
nuxt-admin/
├─ pages/
│  ├─ login.vue
│  ├─ dashboard.vue
│  └─ users/index.vue
├─ layouts/default.vue
├─ store/user.ts
├─ plugins/
│  ├─ element-plus.ts
│  └─ axios.ts
├─ middleware/auth.global.ts
├─ server/api/user.ts
├─ composables/useAuth.ts
├─ app.vue
└─ nuxt.config.ts
```

------

## 💻 关键代码模板

### `/plugins/element-plus.ts`

```
import ElementPlus from 'element-plus'
import 'element-plus/dist/index.css'

export default defineNuxtPlugin((nuxtApp) => {
  nuxtApp.vueApp.use(ElementPlus)
})
```

### `/plugins/axios.ts`

```
import axios from 'axios'

export default defineNuxtPlugin(() => {
  const instance = axios.create({
    baseURL: '/api',
    timeout: 10000,
  })

  return {
    provide: { axios: instance }
  }
})
```

### `/store/user.ts`

```
import { defineStore } from 'pinia'

export const useUserStore = defineStore('user', {
  state: () => ({
    token: '',
    userInfo: null
  }),
  actions: {
    setToken(token: string) {
      this.token = token
    },
    logout() {
      this.token = ''
      this.userInfo = null
    }
  }
})
```

### `/middleware/auth.global.ts`

```
import { useUserStore } from '~/store/user'

export default defineNuxtRouteMiddleware((to) => {
  const userStore = useUserStore()
  if (!userStore.token && to.path !== '/login') {
    return navigateTo('/login')
  }
})
```

------

## 📆 开发计划

| Day  | 内容                          | 目标         |
| ---- | ----------------------------- | ------------ |
| 1    | 初始化项目、安装 Element Plus | 运行环境搭建 |
| 2    | 登录页 + Pinia 登录状态       | 认证机制     |
| 3    | 动态菜单 + Layout 框架        | SSR 布局     |
| 4    | Axios 封装 + Mock 接口        | 数据请求     |
| 5    | 权限中间件                    | 安全控制     |
| 6    | 用户列表页 + 分页             | CRUD         |
| 7    | 打包 & 部署到 Vercel          | 实战上线     |

------

# 🥈 项目二：Nuxt3 + Supabase 博客系统

## 🎯 目标

构建一个完整的 SSR 博客系统（支持登录、发帖、编辑、SEO）

------

## 🧩 技术栈

- Nuxt3
- Supabase（Auth + Database）
- TailwindCSS
- Markdown 解析（`@nuxt/content`）

------

## ⚙️ 安装命令

```
npx nuxi init nuxt-supabase-blog
cd nuxt-supabase-blog
npm install @supabase/supabase-js tailwindcss @nuxt/content
npx tailwindcss init -p
```

------

## 📁 目录结构

```
nuxt-supabase-blog/
├─ pages/
│  ├─ index.vue
│  ├─ post/[id].vue
│  ├─ auth/login.vue
│  └─ admin/new.vue
├─ composables/useSupabase.ts
├─ plugins/supabase.client.ts
├─ content/
│  └─ hello-world.md
└─ nuxt.config.ts
```

------

## 💻 核心代码模板

### `/plugins/supabase.client.ts`

```
import { createClient } from '@supabase/supabase-js'

export default defineNuxtPlugin(() => {
  const config = useRuntimeConfig()
  const supabase = createClient(config.public.supabaseUrl, config.public.supabaseAnonKey)
  return { provide: { supabase } }
})
```

### `/composables/useSupabase.ts`

```
export const useSupabaseClient = () => {
  const { $supabase } = useNuxtApp()
  return $supabase
}
```

### `/pages/index.vue`

```
<script setup>
const { data: posts } = await useAsyncData('posts', async () => {
  const { $supabase } = useNuxtApp()
  const { data } = await $supabase.from('posts').select('*')
  return data
})
</script>

<template>
  <div class="p-8">
    <h1>My Supabase Blog</h1>
    <ul>
      <li v-for="post in posts" :key="post.id">
        <NuxtLink :to="`/post/${post.id}`">{{ post.title }}</NuxtLink>
      </li>
    </ul>
  </div>
</template>
```

------

## 📆 开发计划

| Day  | 内容                     |
| ---- | ------------------------ |
| 1    | 搭建项目、配置 Tailwind  |
| 2    | 集成 Supabase + 环境变量 |
| 3    | 文章列表页（SSR）        |
| 4    | 文章详情页（Markdown）   |
| 5    | 登录/注册功能            |
| 6    | 后台发帖页面             |
| 7    | SEO + 部署               |

------

# 🥉 项目三：Nuxt3 + Shopify API 前台展示

## 🎯 目标

实现电商前台页面，调用 Shopify Storefront API 展示商品。

------

## 🧩 技术栈

- Nuxt3
- Shopify Storefront GraphQL API
- Apollo Client
- TailwindCSS

------

## ⚙️ 安装命令

```
npx nuxi init nuxt-shopify
cd nuxt-shopify
npm install @apollo/client graphql tailwindcss
npx tailwindcss init -p
```

------

## 📁 目录结构

```
nuxt-shopify/
├─ pages/
│  ├─ index.vue
│  ├─ products/[handle].vue
│  └─ cart.vue
├─ plugins/apollo.client.ts
├─ composables/useShopify.ts
├─ store/cart.ts
└─ nuxt.config.ts
```

------

## 💻 核心代码模板

### `/plugins/apollo.client.ts`

```
import { ApolloClient, InMemoryCache, HttpLink } from '@apollo/client/core'

export default defineNuxtPlugin(() => {
  const link = new HttpLink({
    uri: 'https://your-shopify-store.myshopify.com/api/2024-07/graphql.json',
    headers: { 'X-Shopify-Storefront-Access-Token': 'your-token' }
  })

  const client = new ApolloClient({ cache: new InMemoryCache(), link })
  return { provide: { apollo: client } }
})
```

### `/composables/useShopify.ts`

```
import gql from 'graphql-tag'

export const useShopify = () => {
  const { $apollo } = useNuxtApp()
  const fetchProducts = async () => {
    const { data } = await $apollo.query({
      query: gql`{ products(first: 10) { edges { node { id title handle } } } }`
    })
    return data.products.edges.map(e => e.node)
  }
  return { fetchProducts }
}
```

------

## 📆 开发计划

| Day  | 内容                      |
| ---- | ------------------------- |
| 1    | 初始化 + Tailwind         |
| 2    | 集成 Apollo + Shopify API |
| 3    | 商品列表页                |
| 4    | 商品详情页                |
| 5    | 购物车状态管理（Pinia）   |
| 6    | 搜索功能                  |
| 7    | 性能优化 + SSG 导出       |

------

# 🏅 项目四：Nuxt3 + i18n + Pinia 多语言网站

## 🎯 目标

构建一个支持中英切换的企业官网模板，兼顾 SSR 与 SEO。

------

## 🧩 技术栈

- Nuxt3
- `@nuxtjs/i18n`
- Pinia
- TailwindCSS

------

## ⚙️ 安装命令

```
npx nuxi init nuxt-i18n-site
cd nuxt-i18n-site
npm install @nuxtjs/i18n pinia tailwindcss
npx tailwindcss init -p
```

------

## 📁 目录结构

```
nuxt-i18n-site/
├─ pages/
│  ├─ index.vue
│  ├─ about.vue
│  └─ contact.vue
├─ locales/
│  ├─ en.json
│  └─ zh.json
├─ store/settings.ts
└─ nuxt.config.ts
```

------

## 💻 核心代码模板

### `/nuxt.config.ts`

```
export default defineNuxtConfig({
  modules: ['@nuxtjs/i18n'],
  i18n: {
    locales: ['en', 'zh'],
    defaultLocale: 'en',
    vueI18n: './i18n.config.ts'
  }
})
```

### `/i18n.config.ts`

```
export default defineI18nConfig(() => ({
  legacy: false,
  locale: 'en',
  messages: {
    en: { hello: 'Hello', about: 'About Us' },
    zh: { hello: '你好', about: '关于我们' }
  }
}))
```

------

## 📆 开发计划

| Day  | 内容                     |
| ---- | ------------------------ |
| 1    | 初始化 + Tailwind        |
| 2    | 配置 i18n 国际化         |
| 3    | 多语言页面               |
| 4    | SEO meta 配置            |
| 5    | Pinia 状态（语言、主题） |
| 6    | 主题切换（亮/暗）        |
| 7    | 部署 Vercel              |

------

## 🚀 最终结果

完成后你将拥有：

1. SSR 后台模板
2. 博客 + 后台管理系统
3. 电商前台展示站
4. 多语言官网模板

这四个项目组合，能覆盖 **Nuxt3 全生态（SSR / SSG / API / i18n / GraphQL / Supabase）**，
 几乎相当于一整套 Nuxt 进阶课程。