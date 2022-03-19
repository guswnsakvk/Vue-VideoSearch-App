<template>
  <div class="moviePoster" :style="{backgroundImage : `url(${movie.large_cover_image})`}">
    <div class="movieDescription">
      <p class="movieTitle">{{movie.title}}</p>
      <p class="movieYear">{{movie.year}}</p>
    </div>
  </div>
</template>

<script>
export default {
  name: 'SearchResult',
  props: {
    movie: Object
  }
}
</script>

<style>
.moviePoster{
  margin-top: 20px;
  margin-right: 10px;
  box-sizing: border-box;
  width: 230px;
  height: 300px;
  background-size: 100% auto;
  background-repeat: no-repeat;
  position: relative;
}

.movieDescription{
  position: absolute;
  width: calc(100% - 20px);
  height: 55px;
  bottom: 0;
  color: #fff;
  font-size: 16px;
  font-weight: 700;
  padding: 10px;
  background: linear-gradient(0deg, rgba(0,0,0,1) 30%, rgba(255,255,255,0) 100%);
}

.movieTitle{
  margin-left: 10px;
  margin-bottom: 5px;
}

.movieYear{
  margin-left: 10px;
}
</style>