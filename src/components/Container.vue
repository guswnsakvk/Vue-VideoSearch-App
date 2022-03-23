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
      this.selectedVideo = response
      console.log(this.selectedVideo)
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