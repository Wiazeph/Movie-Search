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
  <div
    class="movies grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 xl:grid-cols-4 gap-4 lg:gap-6 xl:gap-8"
  >
    <div
      class="movie p-5 w-full bg-[#2a2c3c] rounded-lg flex flex-col items-center justify-center gap-4 border-[#3d3d50] border-[3px] border-solid"
      v-for="result in setresults"
      :key="result.id"
    >
      <div class="movie-img w-full relative overflow-hidden group">
        <img
          class="w-full"
          :src="'http://image.tmdb.org/t/p/w500/' + result.poster_path"
        />
        <div
          class="movie-info absolute z-10 -bottom-full left-0 w-full h-full transition-all duration-300 ease-in-out group-hover:bottom-0 bg-[linear-gradient(0deg,rgb(0,0,0)_0%,rgba(0,0,0,0)_100%)]"
        >
          <div
            class="movie-info-details absolute bottom-3 left-3 z-20 flex flex-col gap-3 w-3/4"
          >
            <div class="movie-title text-lg text-[#efc700]">
              {{ result.original_title }}
            </div>
            <div
              class="movie-info-genre flex gap-x-2 md:gap-x-3 gap-y-1 flex-wrap"
            >
              <span
                class="genres"
                v-for="(category, index) in categoryFilter(result.genre_ids)"
                :key="index"
                >{{ category.name }}
              </span>
            </div>
            <div class="movie-info-date">
              {{ result.release_date }}
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped></style>
