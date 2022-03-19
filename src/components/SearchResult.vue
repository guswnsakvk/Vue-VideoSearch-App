<template>
  <div class="moviePosterBox"></div>
</template>

<script>
export default {
  name: 'SearchResult',
  props: {
    movieList: Array
  }
}
</script>

<style>
.moviePosterBox{
  background-color: red;
  box-sizing: border-box;
  width: 220px;
  height: 300px;
}
</style>