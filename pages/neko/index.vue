<script setup lang="ts">
const { data, refresh } = await useAsyncData(
  'neko',
  () => $fetch<{
    result: Array<any>
  }>('https://nekos.best/api/v2/neko'),
)
</script>

<template>
  <div>
    <button @click="refresh()">
      刷新
    </button>
    <img :src="data?.result[0].url" class="w-[400px]">
  </div>
</template>

<style scoped>

</style>
