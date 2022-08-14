<template>
  <div>
    <VideoView
      :display="videoShowValue"
      :movieId="videos"
      @close="videoClose"
    />
    <SignView :display="modalShowValue" @close="modalClose" />
    <!-- =============== START OF RESPONSIVE - MAIN NAV =============== -->
    <nav id="main-mobile-nav"></nav>
    <!-- =============== END OF RESPONSIVE - MAIN NAV =============== -->

    <!-- =============== START OF WRAPPER =============== -->
    <div class="wrapper">
      <!-- =============== START OF HEADER NAVIGATION =============== -->
      <!-- Insert the class "sticky" in the header if you want a sticky header -->
      <HeaderView @show="modalShow" @searchMovie="searchMovie" />
      <!-- =============== START OF SLIDER REVOLUTION SECTION =============== -->
      <SliderView @hideMain="hideMain" />
      <!-- =============== START OF SLIDER REVOLUTION SECTION =============== -->
      <!-- 검색 후 나타내는 페이지 -->
      <section class="top-movies2 search active">
        <div class="container">
          <div class="row" v-if="searchResult.length > 0">
            <!-- Movie List Item -->
            <div
              class="col-lg-3 col-md-6 col-sm-6 col-xs-12"
              v-for="(item, i) in searchResult"
              :key="i"
            >
              <div>
                <div class="movie-box-4">
                  <div class="listing-container">
                    <!-- Movie List Image -->
                    <div class="listing-image">
                      <!-- Buttons -->
                      <div class="buttons">
                        <a
                          href="javascript:void(0)"
                          data-original-title="Rate"
                          data-toggle="tooltip"
                          data-placement="bottom"
                          class="like"
                        >
                          <i class="icon-heart"></i>
                        </a>

                        <a
                          href="javascript:void(0)"
                          data-original-title="Share"
                          data-toggle="tooltip"
                          data-placement="bottom"
                          class="share"
                        >
                          <i class="icon-share"></i>
                        </a>
                      </div>

                      <!-- Rating -->
                      <div class="stars">
                        <div class="rating">
                          <i
                            class="fa fa-star"
                            v-for="(num, i) in parseInt(item.vote_average / 2)"
                            :key="'star' + i"
                          ></i>
                          <i
                            class="fa fa-star-o"
                            v-for="(num, i) in 5 -
                            parseInt(item.vote_average / 2)"
                            :key="'no-star' + i"
                          ></i>
                        </div>
                      </div>

                      <!-- Image -->
                      <img
                        :src="`https://image.tmdb.org/t/p/w200/${item.poster_path}`"
                        alt=""
                      />
                    </div>

                    <!-- Movie List Content -->
                    <div class="listing-content">
                      <div class="inner">
                        <h2 class="title">{{ item.title }}</h2>

                        <router-link
                          :to="`/detail/${item.id}`"
                          class="btn btn-main btn-effect"
                          >상세보기</router-link
                        >
                      </div>
                    </div>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>
      </section>
      <FooterView />
    </div>
    <!-- =============== END OF WRAPPER =============== -->
  </div>
</template>

<script>
import HeaderView from "@/components/HeaderView.vue";
import FooterView from "@/components/FooterView.vue";
import SliderView from "@/components/Main/SliderView.vue";
import SignView from "@/components/Main/SignView.vue";
import VideoView from "@/components/Main/VideoView.vue";
import axios from "axios";
export default {
  components: {
    HeaderView,
    FooterView,
    SliderView,
    SignView,
    VideoView,
  },
  data() {
    return {
      movieList: {
        popular: [],
        nowPlay: [],
        genre: [],
      },
      upComing: {
        upComing: [],
        upComingId: 0,
        upComingTitle: [],
        upComingReleaseDate: [],
      },

      modalShowValue: false,
      videoShowValue: false,
      videoId: 0,
      videos: "",
      showMovie: false,
      totalMovies: [],
      totalTvs: [],
      cntMovie: 0,
      cntTv: 0,
      cntUser: 0,
      raf: null,
      timestart: null,
      currentTime: 0,

      search: "",
      searchResult: [],
    };
  },
  mounted() {
    const i = Math.floor(Math.random() * 11);
    this.i = i;
  },
  methods: {
    modalShow() {
      return (this.modalShowValue = true);
    },
    modalClose() {
      return (this.modalShowValue = false);
    },

    async videoShow(i, str) {
      if (str === "latest") {
        this.videoId = this.movieList.nowPlay[i].id;
      } else {
        this.videoId = this.upComing.upComing[this.i + i].id;
      }

      this.videoShowValue = true;
      const video = await axios({
        method: "get",
        url: `https://api.themoviedb.org/3/movie/${this.videoId}/videos?api_key=0bb0b51dbb47771a2b73398672aac6cf&region=kr&language=ko`,
      });
      try {
        this.videos = video.data.results[0].key;
      } catch (error) {
        this.videoShowValue = false;
      }
    },

    videoClose() {
      return (this.videoShowValue = false);
    },

    // 검색하면 메인 부분 숨김처리 후 검색내용 출력
    hideMain() {
      this.showMovie = true;
    },

    searchMovie(event) {
      event.preventDefault();

      this.showMovie = true;
    },
  },
  async created() {
    const popular = await axios({
      method: "get",
      url: "https://api.themoviedb.org/3/movie/popular?api_key=0bb0b51dbb47771a2b73398672aac6cf&region=kr&language=ko",
    });
    this.movieList.popular = popular.data.results;

    const nowPlay = await axios({
      method: "get",
      url: "https://api.themoviedb.org/3/movie/now_playing?api_key=0bb0b51dbb47771a2b73398672aac6cf&region=kr&language=ko",
    });
    this.movieList.nowPlay = nowPlay.data.results;

    const genre = await axios({
      method: "get",
      url: "https://api.themoviedb.org/3/genre/movie/list?api_key=0bb0b51dbb47771a2b73398672aac6cf&language=ko",
    });
    this.movieList.genre = genre.data.genres;

    const upComing = await axios({
      method: "get",
      url: "https://api.themoviedb.org/3/movie/upcoming?api_key=0bb0b51dbb47771a2b73398672aac6cf&region=kr&language=ko",
    });
    this.upComing.upComing = upComing.data.results;

    const totalMovie = await axios({
      method: "get",
      url: "https://api.themoviedb.org/3/discover/movie?api_key=3d6c850fedd64a507e51cfb2335f305c&language=ko",
    });
    this.totalMovies = totalMovie.data.total_results;

    const totalTv = await axios({
      method: "get",
      url: "https://api.themoviedb.org/3/discover/tv?api_key=3d6c850fedd64a507e51cfb2335f305c&language=ko",
    });
    this.totalTvs = totalTv.data.total_results;

    const searchApi = await axios({
      method: "get",
      url: `https://api.themoviedb.org/3/search/movie?api_key=3d6c850fedd64a507e51cfb2335f305c&query=${this.$route.params.idx}&language=ko&region=kr`,
    });
    this.searchResult = searchApi.data.results;
  },
  computed: {},
};
</script>

<style scoped>
.upcoming-movies {
  /* background: url("@/assets/images/posters/movie-collection.jpg"); */
  background-attachment: fixed;
  background-color: rgb(62, 69, 85);
  opacity: 0.95;
}

.line-clamp {
  display: -webkit-box;
  -webkit-line-clamp: 3;
  -webkit-box-orient: vertical;
  overflow: hidden;
}

.search {
  display: none;
}

.search.active {
  display: block;
}

.col-md-6 {
  margin-bottom: 2.3%;
}
</style>
