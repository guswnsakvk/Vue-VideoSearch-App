<template>
  <div class="movieBox">
    <SearchResult v-for="video in videoList" :key="video" :video = video />
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
   videoList: Array
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