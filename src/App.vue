<script setup>
import { ref } from "vue";
import axios from "axios";

import SearchBar from "./components/SearchBar.vue";
import MovieLists from "./components/MovieLists.vue";

const genres = ref(null);
const results = ref([]);

const getGenres = () =>
  axios
    .get(
      "https://api.themoviedb.org/3/genre/movie/list?api_key=ce69cf9a4d49e89a157595ab1e34c07e&language=en-US"
    )
    .then((response) => {
      genres.value = response.data.genres;
    });
getGenres();
</script>

<template>
  <header
    class="mt-4 sm:mt-6 md:mt-8 lg:mt-10 xl:mt-12 mb-10 sm:mb-12 md:mb-14 lg:mb-16 xl:mb-20 flex-col gap-8 sm:gap-9 md:gap-10 lg:gap-11 xl:gap-12"
  >
    <SearchBar
      @get-results="
        (content) => {
          results = content;
        }
      "
    />
  </header>

  <main class="mb-4 sm:mb-6 md:mb-8 lg:mb-10 xl:mb-12">
    <MovieLists v-if="genres" :setresults="results" :category="genres" />
  </main>
</template>

<style scoped></style>
