<script>
import { ref, watchEffect } from "vue"
const animeRecent = ref([])

watchEffect(async () => {
  await fetch(`https://gogoanime.consumet.org/recent-release`)
    .then((res) => res.json())
    .then((data) => (animeRecent.value = data))
    .catch((err) => console.error(err))
  console.log(animeRecent.value)
})
</script>

<template>
  <div
    class="w-full grid grid-cols-2 md:grid-cols-3 lg:grid-cols-4 items-center justify-center"
  >
    <Card v-for="anime in animeRecent" :key="anime.animeId" :anime="anime" />
  </div>
</template>
