<script>
import { ref, watchEffect } from "vue"
const animePopular = ref([])

watchEffect(async () => {
  await fetch(`https://gogoanime.consumet.org/popular`)
    .then((res) => res.json())
    .then((data) => (animePopular.value = data))
    .catch((err) => console.error(err))
  console.log(animePopular.value)
})
</script>

<template>
  <div
    class="w-full grid grid-cols-2 md:grid-cols-3 lg:grid-cols-4 items-center justify-center"
  >
    <Card v-for="anime in animePopular" :key="anime.animeId" :anime="anime" />
  </div>
</template>
