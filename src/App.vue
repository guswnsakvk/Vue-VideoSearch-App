<template>
  <div class="header">
    <div class="webName" @click="likeMovieList(1), videoList = [], selectedGenres = '', nowPage = 1">
      <span>content searcher</span>
      <p class="webTitle">Video Finder</p>
    </div>
  </div>

  <div class="search_area">
    <form @submit.prevent="searchVideo(1), videoList=[], selectedGenres = '', nowPage = 1">
      <input v-model="videoName" required class="search_bar" type="text" placeholder="Search for the title of the content">
      <button type="submit" class="fa-solid fa-magnifying-glass searchIcon"></button>
    </form>
  </div>
  
  <div class="btnContainer" v-if="!selected">
    <Genres @passChoseGenres = getChoseGenres v-for="genres in genresList" :key="genres" :genres = genres :selectedGenres = selectedGenres />
  </div>

  <Container @passSelected = getSelected :videoList = videoList :selected = selected />
</template>

<script>
import axios from 'axios'
import Container from './components/Container.vue'
import Genres from './components/Genres.vue'

export default {
  name: 'App',
  data(){
    return{
      videoList : [],
      videoName : '' ,
      nowPage : 1,
      lastPage : 0,
      search : false,
      selected : false,
      genresList : ['Action', 'Adventure', 'Comedy', 'Sci-Fi', 'Crime', 'Thriller'],
      selectedGenres : ''
    }
  },
  components: {
    Container,
    Genres
  },
  methods: {
    searchVideo(page){
      this.search = true
      this.selected = false
      axios
        .get(`https://yts.mx/api/v2/list_movies.json?query_term=${this.videoName}&limit=25&page=${page}&genre=${this.selectedGenres}`)
        .then((response) => {
          this.lastPage = Math.ceil(response.data.data.movie_count / 25)
          for (let i=0; i<response.data.data.movies.length;i++){
            this.videoList.push(response.data.data.movies[i])
        }
      })
    },
    likeMovieList(page){
      this.search = false
      this.selected = false
      axios
        .get(`https://yts.mx/api/v2/list_movies.json?sort_by=like_count&limit=25&page=${page}&genre=${this.selectedGenres}`)
        .then((response) => {
          this.lastPage = Math.ceil(response.data.data.movie_count / 25)
          for (let i=0; i<response.data.data.limit;i++){
            this.videoList.push(response.data.data.movies[i])
        }
      })
    },
    onScroll(){
      if(!this.selected){
        if(this.search){
          if((window.innerHeight + window.scrollY) >= document.body.offsetHeight && this.lastPage > this.nowPage){
            this.nowPage += 1
            this.searchVideo(this.nowPage)
          }
        }
        else{
          if((window.innerHeight + window.scrollY) >= document.body.offsetHeight && this.lastPage > this.nowPage){
            this.nowPage += 1
            this.likeMovieList(this.nowPage)
          }
        }
      }
    },
    getSelected(response){
      this.selected = response
    },
    getChoseGenres(response){
      this.videoList = []
      // if(this.selectedGenres.includes(response)){
      //   this.selectedGenres = this.selectedGenres.filter((element) => element != response)
      // }else{
      //   this.selectedGenres.push(response)
      // }

      this.selectedGenres =  response
      console.log(this.selectedGenres)

      if(this.search){
        this.searchVideo(1)
      }else{
        this.likeMovieList(1)
      }
    }
    
  },
  mounted(){
    this.$nextTick(function(){
      this.nowPage = 1
      axios
        .get('https://yts.mx/api/v2/list_movies.json?sort_by=like_count&limit=25')
        .then((response) => {
          this.lastPage = Math.ceil(response.data.data.movie_count / 25)
          for (let i=0; i<response.data.data.limit;i++){
            this.videoList.push(response.data.data.movies[i])
        }
      })
    })
    window.addEventListener('scroll', this.onScroll)
  },
  beforeUnmount(){
    window.removeEventListener('scroll', this.onScroll)
  },
}
</script>

<style>
.btnContainer{
  display: flex;
  flex-wrap: wrap;
  margin-top: 20px;
}

.search_bar{
  width: 100%;
  height: 36px;
  background-color: #141414;
  border: none;
  color: #999;
  font-size: 20px;
  border-radius: 7px;
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
  right: 0px;
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

.webName{
  display: flex;
  cursor: pointer;
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
