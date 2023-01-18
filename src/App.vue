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
  <header>
    <SearchBar
      @get-results="
        (content) => {
          results = content;
        }
      "
    />
  </header>

  <main>
    <MovieLists v-if="genres" :setresults="results" :category="genres" />
  </main>
</template>

<style scoped></style>
