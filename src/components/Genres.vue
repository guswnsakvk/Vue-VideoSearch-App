<template>
  <!-- 비디오 장르를 보여줌
  선택한 장르를 App.vue에 전달 -->
  <div>
    <div @click="choseGenres(genres)" class="genresBtn">#{{ genres }}</div>
  </div>
</template>

<script>
export default {
  name: "Generes",
  methods: {
    choseGenres(genres) {
      this.$emit("passChoseGenres", genres);
    },
  },
  props: {
    genres: String,
    selectedGenres: String,
  },
};
</script>

<style>
.genresBtn {
  color: #fff;
  font-size: 18px;
  background-color: #a734ff;
  width: 110px;
  height: 30px;
  text-align: center;
  border-radius: 15px;
  line-height: 30px;
  margin-right: 20px;
  margin-bottom: 10px;
  cursor: pointer;
}

@media screen and (max-width: 576px) {
  .genresBtn {
    font-size: 16px;
    width: 100px;
  }
}
</style>
