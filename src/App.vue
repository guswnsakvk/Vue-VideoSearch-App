<template>
  <div class="header">
    <div
      class="webName"
      @click="setValue(false), homeVideoList(1), (videoName = '')"
    >
      <span>content searcher</span>
      <p class="webTitle">Video Finder</p>
    </div>
  </div>

  <div class="search_area">
    <form @submit.prevent="setValue(true), searchVideo(1)">
      <input
        v-model="videoName"
        required
        class="search_bar"
        type="text"
        placeholder="Search for the title of the content"
      />
      <button
        type="submit"
        class="fa-solid fa-magnifying-glass searchIcon"
      ></button>
    </form>
  </div>

  <div class="btnContainer" v-if="!selected">
    <Genres
      @passChoseGenres="getChoseGenres"
      v-for="genres in genresList"
      :key="genres"
      :genres="genres"
      :selectedGenres="selectedGenres"
    />
  </div>

  <Container
    @passSelected="getSelected"
    :videoList="videoList"
    :selected="selected"
  />
</template>

<script>
import axios from "axios";
import Container from "./components/Container.vue";
import Genres from "./components/Genres.vue";
export default {
  name: "App",
  data() {
    return {
      videoList: [], // 비디오 목록 저장
      videoName: "", // 비디오 이름 저장
      nowPage: 1, // 현재 페이지
      lastPage: 0, // 검색한 비디오 목록 마지막 페이지
      search: false, // 비디오 이름으로 검색했는 지 확인
      selected: false, // 비디오 포스터를 클릭했는 지 확인
      genresList: [
        // 비디오 장르 목록
        "Action",
        "Adventure",
        "Comedy",
        "Sci-Fi",
        "Crime",
        "Thriller",
      ],
      selectedGenres: "", // 장르를 선택했는 지 확인
    };
  },
  components: {
    Container,
    Genres,
  },
  methods: {
    // 비디오 이름으로 검색할 경우
    // 비디오 이름과 선택한 장르로 검색
    async searchVideo(page) {
      await axios
        .get(
          `https://yts.mx/api/v2/list_movies.json?query_term=${this.videoName}&page=${page}&genre=${this.selectedGenres}`
        )
        .then((response) => {
          this.setVideoList(response);
        });
    },
    // 비디오 이름으로 검색하지 않을 경우
    // 선택한 장르를 기준으로 인기 높은 순으로 검색
    async homeVideoList(page) {
      await axios
        .get(
          `https://yts.mx/api/v2/list_movies.json?sort_by=like_count&page=${page}&genre=${this.selectedGenres}`
        )
        .then((response) => {
          this.setVideoList(response);
        });
    },
    // 호출한 비디오 목록 저장
    setVideoList(response) {
      this.lastPage = Math.ceil(response.data.data.movie_count / 25);
      for (let i = 0; i < response.data.data.movies.length; i++) {
        this.videoList.push(response.data.data.movies[i]);
      }
    },
    // searchVideo, homeVideoList 실행시
    // 변경되는 값 변경
    setValue(value) {
      this.videoList = [];
      this.nowPage = 1;
      this.selected = false;
      this.search = value;
      this.selectedGenres = "";
    },
    // 비디오를 선택하지 않을 경우
    // 스크롤을 끝깨지 내릴 시 다음 페이지 목록 검색
    onScroll() {
      if (!this.selected) {
        if (this.search) {
          if (
            window.innerHeight + window.scrollY >=
              document.body.offsetHeight - 10 &&
            this.lastPage > this.nowPage
          ) {
            this.nowPage += 1;
            this.searchVideo(this.nowPage);
          }
        } else {
          if (
            window.innerHeight + window.scrollY >=
              document.body.offsetHeight - 10 &&
            this.lastPage > this.nowPage
          ) {
            this.nowPage += 1;
            this.homeVideoList(this.nowPage);
          }
        }
      }
    },
    // 비디오를 선택할 경우
    // true로 변경
    getSelected(response) {
      this.selected = response;
    },
    // 장르를 선택할 경우
    // 장르 저장
    getChoseGenres(response) {
      this.videoList = [];
      this.selectedGenres = response;
      if (this.search) {
        this.searchVideo(1);
      } else {
        this.homeVideoList(1);
      }
    },
  },
  mounted() {
    // 페이지를 처음에 들어갈 경우
    // 인기 순으로 비디오 목록 검색
    this.homeVideoList(1);
    window.addEventListener("scroll", this.onScroll);
  },
  beforeUnmount() {
    window.removeEventListener("scroll", this.onScroll);
  },
};
</script>

<style>
.btnContainer {
  display: flex;
  flex-wrap: wrap;
  margin-top: 20px;
}
.search_bar {
  width: 100%;
  height: 36px;
  background-color: #141414;
  border: none;
  color: #999;
  font-size: 20px;
  border-radius: 7px;
}
.search_area {
  height: 36px;
  width: 100%;
  position: relative;
  flex-direction: column;
}
button {
  background-color: transparent;
  border: none;
  cursor: pointer;
}
.searchIcon {
  color: #fff;
  position: absolute;
  width: 50px;
  height: 50px;
  top: -5px;
  right: 0px;
  z-index: 1;
  font-size: 25px;
}
.header {
  width: 100%;
  height: 50px;
  line-height: 50px;
  color: #999;
  display: flex;
  font-size: 20px;
}
.webName {
  display: flex;
  cursor: pointer;
}
.webTitle {
  margin-left: 5px;
  color: #a734ff;
}
body {
  background-color: #141414;
}
#app {
  width: 100%;
  max-width: 1200px;
  margin: auto;
}

@media screen and (max-width: 576px) {
  .header {
    margin-left: 15px;
  }

  .search_area {
    margin-left: 15px;
    width: 95%;
  }

  .btnContainer {
    margin-left: 15px;
  }

  #app {
    width: 100%;
    max-width: 576px;
    margin: auto;
  }
}
</style>