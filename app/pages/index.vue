<template>
  <div>hello world</div>
  <HelloWorld />
  <NuxtLink to="/about">跳转到about页面</NuxtLink>
  <a-button @click="toAbout">点击跳转</a-button>
</template>

<script setup>
const router = useRouter()
const toAbout = () => {
  router.push({
    path: '/about',
    query: {
      id: 1,
      userName: 'admin',
    }
  })
}
</script>