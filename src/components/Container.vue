<template>
  <div>
    <!-- 비디오를 선택하지 않았을 경우 -->
    <div v-if="!selected" class="movieBox">
      <SearchResult
        @passDetailData="getDetailData"
        v-for="video in videoList"
        :key="video"
        :video="video"
      />
    </div>

    <!-- 비디오를 선택한 경우 -->
    <div v-if="selected">
      <DeatilVideo :selectedVideo="selectedVideo" />
    </div>
  </div>
</template>

<script>
import SearchResult from "./SearchResult.vue";
import DeatilVideo from "./DeatilVideo.vue";

export default {
  name: "Container",
  data() {
    return {
      selectedVideo: "",
    };
  },
  props: {
    videoList: Array,
    selected: Boolean,
  },
  components: {
    SearchResult,
    DeatilVideo,
  },
  methods: {
    // SearchResult.vue에서 받은 데이터를 저장
    // App.vue에 selected를 true로 바꾸기 위해 true값 전달
    getDetailData(response) {
      this.selectedVideo = response;
      this.$emit("passSelected", true);
    },
  },
};
</script>

<style>
.movieBox {
  display: flex;
  flex-wrap: wrap;
}
</style>
