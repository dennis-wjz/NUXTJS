<template>
  <h1>User:{{ route.params.group }}/{{ route.params.id }}</h1>
</template>

<script setup >
const route = useRoute();
</script>