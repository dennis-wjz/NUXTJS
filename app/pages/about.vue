<template>
  <section>
    <p>此页面将在 /about 路由下显示。</p>
  </section>
  <h1>About:{{ route.query.id }} {{ route.query.userName }}</h1>
</template>

<script setup>
const route = useRoute()
</script>
