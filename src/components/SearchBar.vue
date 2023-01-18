<script setup>
import axios from "axios";
import { ref } from "vue";

const query = ref("");

const emits = defineEmits(["getResults"]);

function getResult(query) {
  axios
    .get(
      "https://api.themoviedb.org/3/search/movie?api_key=ce69cf9a4d49e89a157595ab1e34c07e&query=" +
        query
    )
    .then((response) => {
      emits("getResults", response.data.results);
    });
}
</script>

<template>
  <h1 class="description">
    Using The Movie Database API Movie Search with Axios
  </h1>

  <input
    class="searchBar"
    type="text"
    v-model="query"
    @keyup="getResult(query)"
  />
</template>

<style scoped></style>
