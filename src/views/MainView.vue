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
      <HeaderView @show="modalShow" />
      <!-- =============== START OF SLIDER REVOLUTION SECTION =============== -->
      <SliderView @hideMain="hideMain" />
      <!-- =============== START OF SLIDER REVOLUTION SECTION =============== -->

      <!-- 검색 하면 사라지게 함 -->
      <main class="main" :class="{ active: showMovie }">
        <!-- =============== START OF TOP MOVIES SECTION =============== -->
        <section class="top-movies2">
          <div class="container">
            <div class="row" v-if="movieList.popular.length > 0">
              <!-- Movie List Item -->
              <div
                class="col-lg-3 col-md-6 col-sm-6 col-xs-12"
                v-for="(item, i) in movieList.popular"
                :key="i"
              >
                <div v-if="i < 4">
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
                              v-for="(num, i) in parseInt(
                                item.vote_average / 2
                              )"
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
        <!-- =============== END OF TOP MOVIES SECTION =============== -->

        <!-- =============== END OF COUNTER SECTION =============== -->
        <section class="counter bg-main-gradient ptb50 text-center">
          <div class="container">
            <div class="row" style="justify-content: space-between">
              <!-- 1st Count up item -->
              <div class="col-md-4 col-sm-12">
                <span class="counter-item movie" data-from="0" data-to="964">{{
                  movieCount
                }}</span>
                <h4>Movies</h4>
              </div>

              <!-- 2nd Count up item -->
              <!-- <div class="col-md-4 col-sm-12">
                <span class="counter-item tv" data-from="0" data-to="743"
                  >0</span
                >
                <h4>TV Shows</h4>
              </div> -->

              <!-- 3rd Count up item -->
              <div class="col-md-4 col-sm-12">
                <span class="counter-item user" data-from="0" data-to="1207">{{
                  userCount
                }}</span>
                <h4>Users</h4>
              </div>
            </div>
          </div>
        </section>
        <!-- =============== END OF COUNTER SECTION =============== -->

        <!-- =============== START OF LATEST RELEASES SECTION =============== -->
        <section class="latest-releases bg-light ptb100">
          <div class="container">
            <!-- Start of row -->
            <div class="row justify-content-center">
              <div class="col-md-7 text-center">
                <h2 class="title">최신 영화</h2>
                <h6 class="subtitle">현재 방영중인 영화 목록입니다.</h6>
              </div>
            </div>
            <!-- End of row -->
          </div>
          <!-- End of Container -->

          <!-- Start of Latest Releases Slider -->
          <carousel
            :autoplay="true"
            :nav="false"
            :dots="true"
            :margin="32"
            :items="5"
            class="carousel"
            v-if="movieList.nowPlay.length > 0"
          >
            <!-- === Start of Sliding Item 1 === -->
            <div v-for="(items, i) in movieList.nowPlay" :key="i">
              <div class="item">
                <div class="movie-box-3">
                  <div class="listing-container">
                    <!-- Movie List Image -->
                    <div class="listing-image">
                      <!-- Image -->
                      <img
                        :src="`https://image.tmdb.org/t/p/w200/${items.poster_path}`"
                        alt=""
                      />
                    </div>

                    <!-- Movie List Content -->
                    <div class="listing-content">
                      <div class="inner">
                        <!-- Play Button -->
                        <div class="play-btn latest">
                          <a
                            href="javascript:void(0)"
                            class="play-video"
                            @click="videoShow(i, 'latest')"
                          >
                            <i class="fa fa-play"></i>
                          </a>
                        </div>

                        <h2 class="title">{{ items.title }}</h2>

                        <!-- Rating -->
                        <div class="stars">
                          <div class="rating">
                            <i class="fa fa-star"></i>
                            <span>{{ items.vote_average }}/10</span>

                            <span
                              class="category"
                              v-for="(item, i) in items.genre_ids.length"
                              :key="i"
                            >
                              <span v-if="i < 2">{{
                                genreIdToName(items.genre_ids, i)
                              }}</span>
                            </span>
                          </div>
                        </div>

                        <p class="line-clamp">
                          {{ items.overview }}
                        </p>

                        <router-link
                          :to="`/detail/${items.id}`"
                          class="btn btn-main btn-effect"
                          >상세보기</router-link
                        >
                      </div>
                    </div>
                  </div>
                </div>
              </div>
            </div>
            <!-- === End of Sliding Item 1 === -->
          </carousel>
          <!-- End of Latest Releases Slider -->
        </section>
        <!-- =============== END OF LATEST RELEASES SECTION =============== -->

        <!-- =============== START OF UPCOMING MOVIES SECTION =============== -->
        <section class="upcoming-movies parallax ptb100">
          <div class="parallax-overlay"></div>
          <div class="container">
            <!-- Start of row -->
            <div class="row justify-content-center">
              <div class="col-md-7 text-center">
                <h2 class="title text-white">개봉 예정인 영화</h2>
              </div>
            </div>
            <!-- End of row -->

            <!-- Start of row -->
            <div class="plz">
              <div class="row mt50" v-if="upComing.upComing.length > 0">
                <!-- === Start of Upcoming Featured Movies & TV Shows === -->
                <div class="col-md-8">
                  <!-- Start of Upcoming Featured Item -->
                  <div class="movie-box-1 upcoming-featured-item">
                    <!-- Start of Poster -->
                    <div class="poster" id="upcoming">
                      <div>
                        <img
                          :src="`https://image.tmdb.org/t/p/w500${upComingRand(
                            0,
                            'path'
                          )}`"
                          alt=""
                        />
                      </div>
                    </div>
                    <!-- End of Poster -->

                    <!-- Start of Buttons -->
                    <div class="buttons upcoming">
                      <a
                        href="javascript:void(0)"
                        class="play-video"
                        @click="videoShow(0, 'upcoming')"
                      >
                        <i class="fa fa-play"></i>
                      </a>
                    </div>
                    <!-- End of Buttons -->

                    <!-- Start of Movie Details -->
                    <div class="movie-details">
                      <h4 class="movie-title">
                        <router-link :to="`/detail/${upComingRand(0, 'id')}`">{{
                          upComingRand(0, "title")
                        }}</router-link>
                      </h4>
                      <span class="released"
                        >개봉일:
                        {{ upComingRand(0, "date") }}
                      </span>
                    </div>
                    <!-- End of Movie Details -->
                  </div>
                  <!-- End of Upcoming Featured Item -->
                </div>
                <!-- === End of Upcoming Featured Movies & TV Shows === -->

                <!-- === Start of Upcoming Movies & TV Shows === -->
                <div class="col-md-4">
                  <!-- Start of Upcoming Item 1 -->
                  <div class="movie-box-1 upcoming-item">
                    <!-- Start of Poster -->
                    <div class="poster">
                      <img
                        :src="`https://image.tmdb.org/t/p/w500${upComingRand(
                          1,
                          'path'
                        )}`"
                        alt=""
                      />
                    </div>
                    <!-- End of Poster -->

                    <!-- Start of Buttons -->
                    <div class="buttons upcoming a">
                      <a
                        href="javascript:void(0)"
                        class="play-video"
                        @click="videoShow(1, 'upcoming')"
                      >
                        <i class="fa fa-play"></i>
                      </a>
                    </div>
                    <!-- End of Buttons -->

                    <!-- Start of Movie Details -->
                    <div class="movie-details">
                      <h4 class="movie-title">
                        <router-link :to="`/detail/${upComingRand(1, 'id')}`">{{
                          upComingRand(1, "title")
                        }}</router-link>
                      </h4>
                    </div>
                    <!-- End of Movie Details -->
                  </div>
                  <!-- End of Upcoming Item 1 -->

                  <!-- Start of Upcoming Item 2 -->
                  <div class="movie-box-1 upcoming-item mt20">
                    <!-- Start of Poster -->
                    <div class="poster">
                      <img
                        :src="`https://image.tmdb.org/t/p/w500${upComingRand(
                          2,
                          'path'
                        )}`"
                        alt=""
                      />
                    </div>
                    <!-- End of Poster -->

                    <!-- Start of Buttons -->
                    <div class="buttons upcoming">
                      <a
                        href="javascript:void(0)"
                        class="play-video"
                        @click="videoShow(2, 'upcoming')"
                      >
                        <i class="fa fa-play"></i>
                      </a>
                    </div>
                    <!-- End of Buttons -->

                    <!-- Start of Movie Details -->
                    <div class="movie-details">
                      <h4 class="movie-title">
                        <router-link :to="`/detail/${upComingRand(2, 'id')}`">{{
                          upComingRand(2, "title")
                        }}</router-link>
                      </h4>
                    </div>
                    <!-- End of Movie Details -->
                  </div>
                  <!-- End of Upcoming Item 2 -->
                </div>
                <!-- === End of Upcoming Movies & TV Shows === -->
              </div>
            </div>
            <!-- End of row -->
          </div>
        </section>
        <!-- =============== END OF UPCOMING MOVIES SECTION =============== -->
      </main>
      <!-- =============== END OF SUBSCRIBE SECTION =============== -->

      <FooterView />
    </div>
    <!-- =============== END OF WRAPPER =============== -->

    <!-- =============== START OF GENERAL SEARCH WRAPPER =============== -->
    <div class="general-search-wrapper">
      <form class="general-search" role="search" method="get" action="#">
        <input type="text" placeholder="Type and hit enter..." />
        <span id="general-search-close" class="ti-close toggle-search"></span>
      </form>
    </div>
    <!-- =============== END OF GENERAL SEARCH WRAPPER =============== -->
  </div>
</template>

<script>
import HeaderView from "@/components/HeaderView.vue";
import FooterView from "@/components/FooterView.vue";
import SliderView from "@/components/Main/SliderView.vue";
import SignView from "@/components/Main/SignView.vue";
import VideoView from "@/components/Main/VideoView.vue";
import axios from "axios";
import carousel from "vue-owl-carousel";
export default {
  components: {
    HeaderView,
    FooterView,
    SliderView,
    SignView,
    VideoView,
    carousel,
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
      userCount: 0,
      movieCount: 0,
    };
  },
  mounted() {
    const i = Math.floor(Math.random() * 11);
    this.i = i;
  },
  methods: {
    genreIdToName(ids, i) {
      for (let j = 0; j < this.movieList.genre.length; j++) {
        if (ids[i] === this.movieList.genre[j].id)
          ids[i] = this.movieList.genre[j].name;
      }
      return ids[i];
    },
    upComingRand(e = 0, str = "id") {
      switch (str) {
        case "id":
          return this.upComing.upComing[this.i + e].id;
        case "title":
          return this.upComing.upComing[this.i + e].title;
        case "path":
          if (this.upComing.upComing[this.i + e].backdrop_path !== null) {
            return this.upComing.upComing[this.i + e].backdrop_path;
          } else {
            this.i =
              Math.floor(Math.random() * 11) !== this.i
                ? this.i
                : Math.floor(Math.random() * 11);
            return this.upComingRand(e, str) !== null
              ? this.upComingRand(e, str)
              : this.upComingRand(e, str);
          }
        case "date":
          return this.upComing.upComing[this.i + e].release_date;
      }
    },
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

    // RAF를 이용한 Countup 기능
    animateMovie(timestamp) {
      if (!this.timestart) {
        this.timestart = timestamp;
      }
      this.currentTime = timestamp - this.timestart;

      this.cntMovie = this.cntMovie + 1111;
      this.movieCount = this.cntMovie;
      if (this.cntMovie < this.totalMovies) {
        this.raf = requestAnimationFrame(this.animateMovie);
      } else {
        cancelAnimationFrame(this.animateMovie);
      }
    },
    animateUser(timestamp) {
      if (!this.timestart) {
        this.timestart = timestamp;
      }
      this.currentTime = timestamp - this.timestart;

      this.cntUser = this.cntUser + 11;
      this.userCount = this.cntUser;
      if (this.cntUser < 1706) {
        this.raf = requestAnimationFrame(this.animateUser);
      } else {
        cancelAnimationFrame(this.animateUser);
      }
    },
    countTotal() {
      this.animateMovie();
      this.animateUser();
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
    this.countTotal();
  },
  computed: {},
};
</script>

<style scoped>
.upcoming-movies {
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

.main {
  display: block;
}

.main.active {
  display: none;
}

.col-md-6 {
  margin-bottom: 2.3%;
}
</style>
