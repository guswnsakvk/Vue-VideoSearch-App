<template>
  <div class="header">
    content searcher
    <p class="webTitle">Video Finder</p>
    <div class=""></div>
  </div>

  <div class="search_area">
    <form>
      <input required class="search_bar" type="text" placeholder="Search for the title of the content">
      <button type="submit" class="fa-solid fa-magnifying-glass searchIcon"></button>
    </form>
  </div>

  <Container :movieList = movieList />
</template>

<script>
import axios from 'axios'
import Container from './components/Container.vue'

export default {
  name: 'App',
  data(){
    return{
      movieList : [],
    }
  },
  components: {
    Container
  },
  methods: {
    
  },
  mounted(){
    this.$nextTick(function(){
      axios
        .get('https://yts.mx/api/v2/list_movies.json?sort_by=like_count&limit=25')
        .then((response) => {
          for (let i=0; i<response.data.data.limit;i++){
            this.movieList.push(response.data.data.movies[i])
        }
      })
    })
  }
}
</script>

<style>
.search_bar{
  width: 100%;
  height: 36px;
  background-color: #141414;
  border: none;
  color: #999;
  font-size: 20px;
}

.search_area{
  height: 36px;
  width: 100%;
  position: relative;
  flex-direction: column;
}

button{
  background-color: transparent;
  border: none;
  cursor: pointer;
}

.searchIcon{
  color: #fff;
  position: absolute;
  width: 50px;
  height: 50px;
  top: -5px;
  right: 8px;
  z-index: 1;
  font-size: 25px;
}

.header{
  width: 100%;
  height: 50px;
  line-height: 50px;
  color: #999;
  display: flex;
  font-size: 20px;
}

.webTitle{
  margin-left: 5px;
  color: #a734ff;
}

body{
  background-color: #141414;
}

#app {
  width: 100%;
  max-width: 1200px;
  margin: auto;
}
</style>
