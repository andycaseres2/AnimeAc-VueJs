<script>
export default {
  anime: "anime",
  props: { anime: String },
}
</script>

<template>
  <div class="p-4 rounded-lg w-full flex flex-col items-center justify-center">
    <a
      class="w-full flex flex-col items-center justify-center"
      :href="anime.animeUrl"
      target="__blank"
    >
      <img
        class="w-full h-full aspect-square rounded-lg hover:scale-105 duration-300 shadow-md"
        :src="anime.animeImg"
        :alt="anime.animeTitle"
      />
      <h3 class="pt-3 hover:text-[#42b883] duration-300">
        {{ anime.animeTitle }}
      </h3>
    </a>
  </div>
</template>
