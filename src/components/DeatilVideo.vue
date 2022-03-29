<template>
  <!-- 선택한 비디오의 정보를 보여주는 컴포넌트 -->
  <div class="container">
    <div
      class="videoPoster"
      :style="{ backgroundImage: `url(${selectedVideo.large_cover_image})` }"
    ></div>
    <div class="videoInfo">
      <p class="Title">{{ selectedVideo.title }}</p>
      <p class="yearAndRun">
        {{ selectedVideo.year }} {{ selectedVideo.runtime }}min
      </p>
      <p class="detailTitle">Genres</p>
      <p class="genres">{{ selectedVideo.genres.join(" ") }}</p>
      <p class="detailTitle">Synopsis</p>
      <p class="synopsis">{{ selectedVideo.synopsis }}</p>
      <p class="detailTitle">MappRating</p>
      <p class="mpa">{{ selectedVideo.mpa_rating }}</p>
      <p class="detailTitle">Rating</p>
      <p class="rating">{{ selectedVideo.rating }}</p>
    </div>
  </div>
</template>

<script>
export default {
  name: "DeatilVideo",
  props: {
    selectedVideo: Object,
  },
};
</script>

<style>
.rating {
  color: #999;
}

.synopsis {
  margin-bottom: 30px;
  color: #999;
}

.mpa {
  margin-bottom: 30px;
  color: #999;
}

.detailTitle {
  font-size: 25px;
}

.genres {
  margin-bottom: 30px;
  color: #999;
}

.yearAndRun {
  margin-bottom: 30px;
}

.Title {
  font-size: 50px;
  margin-bottom: 30px;
}

.videoInfo {
  width: 500px;
  margin-left: 50px;
  color: #fff;
  font-size: 20px;
}

.videoPoster {
  width: 400px;
  height: 600px;
  border-radius: 10px;
  background-repeat: no-repeat;
  background-size: 100% auto;
}

.container {
  width: 100%;
  padding: 20px 0 0 80px;
  display: flex;
}

@media screen and (max-width: 576px) {
  .container {
    display: block;
    padding: 20px 0 0 40px;
  }

  .videoPoster {
    width: 320px;
    height: 500px;
  }

  .videoInfo {
    width: 320px;
    margin-left: 10px;
    font-size: 15px;
  }

  .synopsis {
    margin-bottom: 15px;
  }

  .mpa {
    margin-bottom: 15px;
  }

  .detailTitle {
    font-size: 20px;
  }

  .genres {
    margin-bottom: 15px;
  }

  .yearAndRun {
    margin-bottom: 15px;
  }

  .Title {
    font-size: 30px;
    margin-bottom: 15px;
  }
}
</style>
