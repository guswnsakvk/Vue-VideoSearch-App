<template>
  <div class="movieBox">
    <SearchResult v-for="movie in movieList" :key="movie" :movie = movie :movieList = movieList />
  </div>
</template>

<script>
import SearchResult from './SearchResult.vue'

export default {
  name: 'Container',
  data(){
    return{

    }
  },
  props: {
   movieList: Array
  },
  components: {
    SearchResult
  },
}
</script>

<style>
.movieBox{
  display: flex;
  flex-wrap: wrap;
}
</style>