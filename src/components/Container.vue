<template>
  <div>
    <div v-if="!selected" class="movieBox" >
      <SearchResult @passDetailData="getDetailData" v-for="video in videoList" :key="video" :video = video />
    </div>

    <div v-if="selected" class="test">
      <p>{{selectedVideo.title}}</p>
    </div>
  </div>
</template>

<script>
import SearchResult from './SearchResult.vue'

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
    SearchResult
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
.test{
  color: #fff
}

.movieBox{
  display: flex;
  flex-wrap: wrap;
}
</style>