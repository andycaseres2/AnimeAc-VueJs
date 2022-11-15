<script>
import { ref, watchEffect } from "vue"
const animeMovie = ref([])

watchEffect(async () => {
  await fetch(`https://gogoanime.consumet.org/anime-movies`)
    .then((res) => res.json())
    .then((data) => (animeMovie.value = data))
    .catch((err) => console.error(err))
  console.log(animeMovie.value)
})
</script>

<template>
  <div
    class="w-full grid grid-cols-2 md:grid-cols-3 lg:grid-cols-4 items-center justify-center"
  >
    <Card v-for="anime in animeMovie" :key="anime.animeId" :anime="anime" />
  </div>
</template>
