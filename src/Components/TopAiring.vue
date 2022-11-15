<script>
import { ref, watchEffect } from "vue"
const animeTop = ref([])

watchEffect(async () => {
  await fetch(`https://gogoanime.consumet.org/top-airing`)
    .then((res) => res.json())
    .then((data) => (animeTop.value = data))
    .catch((err) => console.error(err))
  console.log(animeTop.value)
})
</script>

<template>
  <div
    class="w-full grid grid-cols-2 md:grid-cols-3 lg:grid-cols-4 items-center justify-center"
  >
    <Card v-for="anime in animeTop" :key="anime.animeId" :anime="anime" />
  </div>
</template>
