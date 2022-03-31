<template>
  <!-- 검색한 비디오의 결과를 보여주는 컴포넌트 -->
  <div
    @click="clickVideoPoster"
    class="moviePoster"
    :style="{ backgroundImage: `url(${video.large_cover_image})` }"
  >
    <div class="movieDescription">
      <p class="movieTitle">{{ video.title }}</p>
      <p class="movieYear">{{ video.year }}</p>
    </div>
  </div>
</template>

<script>
export default {
  name: "SearchResult",
  props: {
    video: Object,
  },
  methods: {
    // 클릭한 비디오 정보 Container.vue로 전달
    clickVideoPoster() {
      this.$emit("passDetailData", this.video);
    },
  },
};
</script>

<style>
.moviePoster {
  margin-top: 20px;
  margin-right: 10px;
  box-sizing: border-box;
  width: 230px;
  height: 300px;
  background-size: 100% auto;
  background-repeat: no-repeat;
  position: relative;
}

.movieDescription {
  position: absolute;
  width: calc(100% - 20px);
  height: 55px;
  bottom: 0;
  color: #fff;
  font-size: 16px;
  font-weight: 700;
  padding: 10px;
  background: linear-gradient(
    0deg,
    rgba(0, 0, 0, 1) 30%,
    rgba(255, 255, 255, 0) 100%
  );
}

.movieTitle {
  margin-left: 10px;
  margin-bottom: 5px;
}

.movieYear {
  margin-left: 10px;
}

@media screen and (max-width: 576px){
  .moviePoster{
    width: 170px;
    height: 220px;
    margin-left: 20px;
    margin-right: 7px;
  }
}
</style>