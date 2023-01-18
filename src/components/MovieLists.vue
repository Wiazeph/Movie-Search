<script setup>
const props = defineProps({
  setresults: {
    type: Array,
    required: true,
  },
  category: {
    type: Array,
    required: true,
  },
});

function categoryFilter(genre_ids) {
  return props.category.filter((category) => genre_ids.includes(category.id));
}
</script>

<template>
  <div class="movies">
    <div class="movie" v-for="result in setresults" :key="result.id">
      <div class="movie-img">
        <img :src="'http://image.tmdb.org/t/p/w500/' + result.poster_path" />
      </div>
      <div class="movie-title">Name: {{ result.original_title }}</div>
      <div class="movie-info">
        <div class="movie-info-date">Date: {{ result.release_date }}</div>
        <div class="movie-info-genre">
          Genre:
          <span
            class="genres"
            v-for="(category, index) in categoryFilter(result.genre_ids)"
            :key="index"
          >
            {{ category.name }}
          </span>
        </div>
        <div class="movie-info-date">
          Language: {{ result.original_language }}
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped></style>
