<script setup>
import { ref } from "vue"
import Card from "./Components/Card.vue"
import Popular from "./Components/Popular.vue"
import Movie from "./Components/Movie.vue"
import RecentRelease from "./Components/RecentRelease.vue"
import TopAiring from "./Components/TopAiring.vue"

const search = ref("")
const animeList = ref([])
const TopList = ref(false)
const PopularList = ref(false)
const MoviesList = ref(false)
const RecentList = ref(false)

// const routes = [{ path: "/", component: Popular }]

const menuList = [
  { menu: "Popular", click: () => (PopularList.value = true) },
  { menu: "Top airing", click: () => (TopList.value = true) },
  { menu: "Recent release", click: () => (RecentList.value = true) },
  { menu: "Movies", click: () => (MoviesList.value = true) },
]

const HandleSearch = async () => {
  await fetch(`https://gogoanime.consumet.org/search?keyw=${search.value}`)
    .then((res) => res.json())
    .then((data) => (animeList.value = data))
    .catch((err) => console.error(err))
  search.value = ""
}
console.log(PopularList.value)
</script>

<template>
  <div class="w-full flex flex-col justify-center items-center py-8 px-4">
    <div class="w-full md:w-5/6 flex flex-col justify-center items-center">
      <header class="pt-14 w-full flex flex-col items-center justify-center">
        <h1 class="text-4xl lg:text-6xl">
          AnimeAc <span class="text-[#42b883]">Vuejs</span>
        </h1>

        <form
          @submit.prevent="HandleSearch"
          class="w-full flex items-center justify-center py-8"
        >
          <input
            type="search"
            placeholder="Search Anime"
            class="w-4/5 md:w-1/2 lg:w-1/3 px-2 bg-transparent border-b border-gray-100 placeholder:text-xl rounded focus:outline-none h-12"
            required
            v-model="search"
          />
        </form>
      </header>

      <div class="w-full flex justify-center items-center pb-8">
        <ul
          v-for="menu in menuList"
          :key="menu"
          class="w-full flex gap-4 justify-center items-center"
        >
          <a @click="menu.click">
            <li
              class="hover:scale-105 hover:text-[#42b883] duration-300 cursor-pointer"
            >
              {{ menu.menu }}
            </li>
          </a>
        </ul>
      </div>

      <div v-if="PopularList">
        <Popular />
      </div>

      <!-- Search -->
      <div
        class="w-full grid grid-cols-2 md:grid-cols-3 lg:grid-cols-4 items-center justify-center"
        v-if="animeList.length > 0"
      >
        <Card v-for="anime in animeList" :key="anime.animeId" :anime="anime" />
      </div>
    </div>
  </div>
</template>
