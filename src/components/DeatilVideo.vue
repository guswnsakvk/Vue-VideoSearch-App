<template>
  <div class="deatilVideoContainer">
    <div class="leftSide">
      <div class="detailVideoPoster" :style="{backgroundImage : `url(${selectedVideo.large_cover_image})`}"></div>
      <div class="detailVideoInfo">
        <div class="videoInfo">
          <div class="infoTitle">Rating</div>
          <div class="infoValue">{{selectedVideo.rating}}</div>
        </div>
        <div class="videoInfo">
          <div class="infoTitle">Genres</div>
          <div class="infoValue">{{selectedVideo.genres.join(' ')}}</div>
        </div>
        <div class="videoInfo">
          <div class="infoTitle">RunTime</div>
          <div class="infoValue">{{selectedVideo.runtime}}min</div>
        </div>
      </div>
    </div>
    
    <div class="rightSide">
      <div class="detailVideoContent">
        <div class="title">
          <span class="videoTitle">{{selectedVideo.title}}</span>
          <span class="videoYear">({{selectedVideo.year}})</span>
        </div>
        <p class="videoSynopsis">{{selectedVideo.synopsis}}</p>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'DeatilVideo',
  data(){
    return{

    }
  },
  props: {
    selectedVideo: Object
  }
  
}
</script>

<style>
.videoSynopsis{
  font-size: 20px;
}

.videoYear{
  font-size: 20px;
}

.videoTitle{
  font-size: 40px;
  margin-bottom: 20px;
}

.title{
  margin-bottom: 20px;
}

.infoValue{
  width: 100%;
}

.rightSide{
  margin-left: 20px;
}

.infoTitle{
  height: 100%;
  width: 110px;
}

.videoInfo{
  width: 100%;
  height: 50px;
  display: flex;
  font-size: 18px;
}

.detailVideoContent{
  width: 650px;
  height: 300px;
  margin-top: 100px;
}

.detailVideoInfo{
  width: 350px;
  height: 100px;
  color: #999;
  margin-top: 10px;
}

.detailVideoPoster{
  width: 350px;
  height: 500px;
  background-size: 100% auto;
}

.deatilVideoContainer{
  margin: auto;
  margin-top: 15px;
  width: 100%;
  max-width: 1100px;
  height: 800px;
  display: flex;
}

.test{
  color: #fff
}
</style>