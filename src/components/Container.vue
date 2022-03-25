<template>
  <div>
    <div v-if="!selected" class="movieBox" >
      <SearchResult @passDetailData="getDetailData" v-for="video in videoList" :key="video" :video = video />
    </div>

    <div v-if="selected" class="test">
      <DeatilVideo :selectedVideo = selectedVideo />
    </div>
  </div>
</template>

<script>
import SearchResult from './SearchResult.vue'
import DeatilVideo from './DeatilVideo.vue'
import axios from 'axios'

export default {
  name: 'Container',
  data(){
    return{
      selectedVideo : ''
    }
  },
  props: {
   videoList: Array,
   selected: Boolean
  },
  components: {
    SearchResult,
    DeatilVideo
  },
  methods: {
    getDetailData(response){
      axios
      this.selectedVideo = response
      console.log(response)
      this.$emit('passSelected', true)
    }
  }
}
</script>

<style>
.movieBox{
  display: flex;
  flex-wrap: wrap;
}
</style>