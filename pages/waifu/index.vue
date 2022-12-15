<script setup lang="ts">
const params = reactive({
  type: 'sfw',
  category: 'awoo',
})
const sfwCategory = [
  'waifu',
  'neko',
  'shinobu',
  'megumin',
  'bully',
  'cuddle',
  'cry',
  'hug',
  'awoo',
  'kiss',
  'lick',
  'pat',
  'smug',
  'bonk',
  'yeet',
  'blush',
  'smile',
  'wave',
  'highfive',
  'handhold',
  'nom',
  'bite',
  'glomp',
  'slap',
  'kill',
  'kick',
  'happy',
  'wink',
  'poke',
  'dance',
  'cringe',
]

const nsfwCategory = [
  'waifu', 'neko', 'trap', 'blowjob',
]

const { data, refresh } = await useAsyncData(
  'waifu',
  () => $fetch<{
    url: string
  }>(`https://api.waifu.pics/${params.type}/${params.category}`),
)
const setParams = (cetegory: string, isSFW: boolean) => {
  params.category = cetegory
  params.type = isSFW ? 'sfw' : 'nsfw'
  refresh()
}
</script>

<template>
  <div>
    <div class="flex items-center gap-1">
      <div v-for="category in sfwCategory" :key="category" @click="setParams(category, true)">
        {{ category }}
      </div>
    </div>
    <div class="flex items-center gap-1">
      <div v-for="category in nsfwCategory" :key="category" class="c" @click="setParams(category, false)">
        {{ category }}
      </div>
    </div>
    <div>{{ data?.url }}</div>
    <button @click="refresh()">
      刷新
    </button>
    <img :src="data?.url" class="w-[400px]">
  </div>
</template>

<style scoped>

</style>
