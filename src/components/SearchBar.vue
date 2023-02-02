<script setup>
import axios from "axios";
import { ref } from "vue";

const query = ref("");

const emits = defineEmits(["getResults"]);

function getResult(query) {
  axios
    .get(
      `https://api.themoviedb.org/3/search/movie?api_key=${
        import.meta.env.VITE_API
      }&query=` + query
    )
    .then((response) => {
      emits("getResults", response.data.results);
    });
}
</script>

<template>
  <h1 class="description text-xl text-center md:text-2xl lg:text-3xl">
    Using The Movie Database API Movie Search with Axios
  </h1>

  <input
    class="searchBar w-full max-w-sm py-2 px-4 outline-none rounded-lg text-gray-900"
    type="text"
    v-model="query"
    @keyup="getResult(query)"
  />
</template>

<style scoped></style>
