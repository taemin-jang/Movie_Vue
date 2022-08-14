<template>
  <div>
    <VideoView
      :display="videoShowValue"
      :movieId="videos"
      :imagePath="imagePath"
      :isType="isType"
      @close="videoClose"
    />
    <!-- =============== START OF RESPONSIVE - MAIN NAV =============== -->
    <nav id="main-mobile-nav"></nav>
    <!-- =============== END OF RESPONSIVE - MAIN NAV =============== -->

    <!-- =============== START OF WRAPPER =============== -->
    <div class="wrapper">
      <!-- =============== START OF HEADER NAVIGATION =============== -->
      <!-- Insert the class "sticky" in the header if you want a sticky header -->
      <HeaderView />
      <!-- =============== END OF HEADER NAVIGATION =============== -->

      <!-- =============== START OF MOVIE DETAIL INTRO =============== -->
      <section
        class="movie-detail-intro overlay-gradient ptb100"
        :style="{
          background:
            'url(' +
            `https://image.tmdb.org/t/p/original/${movieDetail.detail.backdrop_path}` +
            ')',
        }"
      ></section>
      <!-- =============== END OF MOVIE DETAIL INTRO =============== -->

      <!-- =============== START OF MOVIE DETAIL INTRO 2 =============== -->
      <section class="movie-detail-intro2">
        <div class="container">
          <div class="row">
            <div class="col-md-12">
              <div class="movie-poster">
                <img
                  :src="`https://image.tmdb.org/t/p/w300/${movieDetail.detail.poster_path}`"
                  alt=""
                />

                <a class="play-video" @click="videoShow(0, 'main')">
                  <i class="fa fa-play"></i>
                </a>
              </div>

              <div class="movie-details">
                <h3 class="title">{{ movieDetail.detail.title }}</h3>

                <ul class="movie-subtext">
                  <li>
                    {{ parseInt(movieDetail.detail.runtime / 60) }}h
                    {{ movieDetail.detail.runtime % 60 }}min
                  </li>
                  <li>
                    <span
                      v-for="(item, i) in movieDetail.detail.genres"
                      :key="i"
                    >
                      {{ genre(movieDetail.detail.genres, i) }}
                    </span>
                  </li>
                  <li>
                    {{ releaseDate(0) + "년" }}
                    {{ releaseDate(1) + "월" }}
                    {{ releaseDate(2) + "일 개봉" }}
                  </li>
                </ul>

                <a
                  href="javascript:void(0)"
                  class="btn btn-main btn-effect"
                  @click="videoShow(0, 'main')"
                  >trailer</a
                >
                <a href="javascript:void(0)" class="btn rate-movie"
                  ><i class="icon-heart"></i
                ></a>

                <div class="rating mt10">
                  <i
                    class="fa fa-star"
                    v-for="(num, i) in count"
                    :key="'star' + i"
                  ></i>
                  <i
                    class="fa fa-star-o"
                    v-for="(num, i) in 5 - count"
                    :key="'no-star' + i"
                  ></i>
                  <span>{{ movieDetail.detail.vote_count }} Ratings</span>
                </div>
              </div>

              <div class="clearfix"></div>
            </div>
          </div>
        </div>
      </section>
      <!-- =============== End OF MOVIE DETAIL INTRO 2 =============== -->

      <!-- =============== START OF MOVIE DETAIL MAIN SECTION =============== -->
      <section class="movie-detail-main ptb100">
        <div class="container">
          <div class="row">
            <!-- Start of Movie Main -->
            <div class="col-lg-8 col-sm-12">
              <div class="inner pr50">
                <!-- Storyline -->
                <div class="storyline">
                  <h3 class="title">줄거리</h3>

                  <p>
                    {{ movieDetail.detail.overview }}
                  </p>
                </div>

                <!-- Media -->
                <div class="movie-media mt50">
                  <h3 class="title">포스터와 동영상</h3>

                  <ul class="image-gallery isotope">
                    <li
                      class="element"
                      v-for="(item, i) in movieDetail.images"
                      :key="i"
                    >
                      <div v-if="i < 6">
                        <a href="javascript:void(0)" @click="showImage(i)">
                          <img
                            :src="`https://image.tmdb.org/t/p/w300${movieDetail.images[i].file_path}`"
                            class="img-responsive"
                            alt=""
                          />
                        </a>
                      </div>
                    </li>

                    <carousel
                      :autoplay="false"
                      :nav="false"
                      :dots="true"
                      :margin="5"
                      :items="3"
                      class="carousel"
                      v-if="movieDetail.movies.length > 0"
                    >
                      <!-- === Start of Sliding Item 1 === -->
                      <div v-for="(items, i) in movieDetail.movies" :key="i">
                        <div class="item">
                          <div class="movie-box-1">
                            <!-- Start of Poster -->
                            <div class="poster">
                              <img
                                :src="`https://img.youtube.com/vi/${items.key}/mqdefault.jpg`"
                                alt=""
                              />
                            </div>
                            <!-- End of Poster -->

                            <!-- Start of Buttons -->
                            <div class="buttons a">
                              <a
                                class="play-video"
                                @click="videoShow(i, 'add')"
                              >
                                <i class="fa fa-play"></i>
                              </a>
                            </div>
                            <!-- End of Buttons -->
                          </div>
                        </div>
                      </div>
                      <!-- === End of Sliding Item 1 === -->
                    </carousel>
                    <!-- <li
                      class="element"
                      v-for="(item, i) in movieDetail.images"
                      :key="i"
                    >
                      <a href="assets/images/blog/bloglist-1.jpg">
                        <img
                          :src="require(`@/assets/images/blog/bloglist-1.jpg`)"
                          class="img-responsive"
                          alt=""
                        />
                      </a>
                    </li> -->
                  </ul>
                </div>
              </div>
            </div>
            <!-- End of Movie Main -->

            <!-- Start of Sidebar -->
            <div class="col-lg-4 col-sm-12">
              <div class="sidebar">
                <!-- Start of Details Widget -->
                <DetailCom :detail="movieDetail.detail" />
                <!-- End of Details Widget -->

                <!-- Start of Details Widget -->
                <aside class="widget widget-movie-cast">
                  <h3 class="title">출연진</h3>

                  <ul class="cast-wrapper">
                    <li v-for="(item, i) in movieDetail.casts" :key="i">
                      <router-link :to="`/credit/detail/${item.credit_id}`">
                        <span class="circle-img">
                          <img :src="`${castImg(i)}`" alt="" />
                        </span>
                        <h6 class="name">{{ castName(i) }}</h6>
                      </router-link>
                    </li>
                  </ul>

                  <router-link
                    :to="`/credit/${$route.params.idx}`"
                    class="btn btn-main btn-effect mt20"
                    >더보기</router-link
                  >
                </aside>
                <!-- End of Details Widget -->
              </div>
            </div>
            <!-- End of Sidebar -->
          </div>
        </div>
      </section>

      <!--  -->

      <!-- =============== END OF MOVIE DETAIL MAIN SECTION =============== -->

      <!-- =============== START OF RECOMMENDED MOVIES SECTION =============== -->
      <section class="recommended-movies bg-light ptb100">
        <div class="container">
          <!-- Start of row -->
          <div class="row">
            <div class="col-md-8 col-sm-12">
              <h2 class="title">다른 추천 영화</h2>
            </div>
          </div>
          <!-- End of row -->

          <!-- Start of Latest Movies Slider -->
          <carousel
            :autoplay="true"
            :nav="false"
            :dots="true"
            :margin="5"
            :items="5"
            class="carousel"
            v-if="movieDetail.recommendations.length > 0"
          >
            <!-- === Start of Sliding Item 1 === -->
            <div v-for="(recomItem, i) in movieDetail.recommendations" :key="i">
              <div class="item">
                <!-- Start of Movie Box -->
                <div class="movie-box-1">
                  <!-- Start of Poster -->
                  <div class="poster">
                    <img :src="`${recomImg(i)}`" alt="" />
                  </div>
                  <!-- End of Poster -->

                  <!-- Start of Buttons -->
                  <div class="buttons a">
                    <a
                      class="play-video"
                      @click="videoShow(0, 'recom', recomItem.id)"
                    >
                      <i class="fa fa-play"></i>
                    </a>
                  </div>
                  <!-- End of Buttons -->

                  <!-- Start of Movie Details -->
                  <div class="movie-details">
                    <h4 class="movie-title" @click="reload">
                      <router-link :to="`/detail/${recomItem.id}`">{{
                        recomItem.title
                      }}</router-link>
                    </h4>
                    <span class="released">{{ recomItem.release_date }}</span>
                  </div>
                  <!-- End of Movie Details -->

                  <!-- Start of Rating -->
                  <div class="stars">
                    <div class="rating">
                      <i class="fa fa-star"></i>
                      <i class="fa fa-star"></i>
                      <i class="fa fa-star"></i>
                      <i class="fa fa-star"></i>
                      <i class="fa fa-star-half-o"></i>
                    </div>
                    <span>{{ recomItem.vote_average.toFixed(1) }} / 10</span>
                  </div>
                  <!-- End of Rating -->
                </div>
                <!-- End of Movie Box -->
              </div>
            </div>
            <!-- === End of Sliding Item 1 === -->
          </carousel>
          <!-- End of Latest Movies Slider -->
        </div>
      </section>
      <!-- =============== END OF RECOMMENDED MOVIES SECTION =============== -->

      <!-- =============== START OF FOOTER =============== -->
      <FooterView />
      <!-- =============== END OF FOOTER =============== -->
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

    <!-- ===== Start of Back to Top Button ===== -->
    <div id="backtotop">
      <a href="javascript:void(0)"></a>
    </div>
    <!-- ===== End of Back to Top Button ===== -->
  </div>
</template>

<script>
import HeaderView from "@/components/HeaderView.vue";
import FooterView from "@/components/FooterView.vue";
import VideoView from "@/components/Main/VideoView.vue";
import DetailCom from "@/components/Detail/DetailCom.vue";
import carousel from "vue-owl-carousel";
import axios from "axios";
export default {
  components: {
    HeaderView,
    FooterView,
    VideoView,
    DetailCom,
    carousel,
  },
  data() {
    return {
      movieDetail: {
        detail: [],
        images: [],
        movies: [],
        casts: [],
        recommendations: [],
      },
      videoShowValue: false,
      videoId: 0,
      videos: "",
      imagePath: "",
      isType: false,
    };
  },
  methods: {
    genre(item, i) {
      return item[i].name;
    },
    releaseDate(i) {
      return (
        this.movieDetail.detail?.release_date &&
        this.movieDetail.detail.release_date.split("-")[i]
      );
    },

    showImage(i) {
      this.imagePath = this.movieDetail.images[i].file_path;
      this.isType = true;
      this.videoShowValue = true;
    },

    async videoShow(i = 0, str, id = 0) {
      this.videoShowValue = true;
      this.isType = false;
      if (str === "add") {
        // 추가된 비디오 영상
        const video = await axios({
          method: "get",
          url: `https://api.themoviedb.org/3/movie/${this.$route.params.idx}/videos?api_key=0bb0b51dbb47771a2b73398672aac6cf&region=kr&language=ko`,
        });
        try {
          this.videos = video.data.results[i].key;
        } catch (error) {
          this.videos = "#";
        }
      } else if (str === "main") {
        const recom = await axios({
          method: "get",
          url: `https://api.themoviedb.org/3/movie/${this.$route.params.idx}/videos?api_key=0bb0b51dbb47771a2b73398672aac6cf&region=kr&language=ko`,
        });
        try {
          this.videos = recom.data.results[0].key;
        } catch (error) {
          this.videos = "#";
        }
      } else if (str === "recom") {
        const recom = await axios({
          method: "get",
          url: `https://api.themoviedb.org/3/movie/${id}/videos?api_key=0bb0b51dbb47771a2b73398672aac6cf&region=kr&language=ko`,
        });
        try {
          this.videos = recom.data.results[0].key;
        } catch (error) {
          this.videos = "#";
        }
      }
    },

    videoClose() {
      return (this.videoShowValue = false);
    },
    castImg(i) {
      try {
        return (
          "https://image.tmdb.org/t/p/w138_and_h175_face" +
          this.movieDetail.casts[i].profile_path
        );
      } catch (error) {
        return "#";
      }
    },
    castName(i) {
      try {
        return this.movieDetail.casts[i].name;
      } catch (error) {
        return "Non";
      }
    },
    recomImg(idx) {
      try {
        return (
          "https://image.tmdb.org/t/p/w300" +
          this.movieDetail.recommendations[idx].poster_path
        );
      } catch (error) {
        return "https://dummyimage.com/300x450/d6d6d6/ffffff.png&text=Not+Image";
      }
    },
    // 같은 페이지 다른 id 로 이동할 때 페이지 새로고침
    reload() {
      return this.$router.go(this.$router.currentRoute);
    },
  },

  computed: {
    count() {
      //  movieDetail.detail.vote_average / 2
      return 3;
    },
  },

  async created() {
    const detail = await axios({
      method: "get",
      url: `https://api.themoviedb.org/3/movie/${this.$route.params.idx}?api_key=0bb0b51dbb47771a2b73398672aac6cf&region=kr&language=ko`,
    });
    this.movieDetail.detail = detail.data;

    const images = await axios({
      method: "get",
      url: `https://api.themoviedb.org/3/movie/${this.$route.params.idx}/images?api_key=0bb0b51dbb47771a2b73398672aac6cf&region=kr&language=ko`,
    });
    this.movieDetail.images = images.data.posters;

    const movies = await axios({
      method: "get",
      url: `https://api.themoviedb.org/3/movie/${this.$route.params.idx}/videos?api_key=0bb0b51dbb47771a2b73398672aac6cf&region=kr&language=ko`,
    });
    this.movieDetail.movies = movies.data.results;

    const cast = await axios({
      method: "get",
      url: `https://api.themoviedb.org/3/movie/${this.$route.params.idx}/credits?api_key=0bb0b51dbb47771a2b73398672aac6cf&region=kr&language=ko`,
    });
    this.movieDetail.casts = cast.data.cast.filter((v, i) => i < 5);

    const recommendations = await axios({
      method: "get",
      url: `https://api.themoviedb.org/3/movie/${this.$route.params.idx}/recommendations?api_key=0bb0b51dbb47771a2b73398672aac6cf&region=kr&language=ko`,
    });
    this.movieDetail.recommendations = recommendations.data.results;
  },
};
</script>

<style lang="scss" scoped></style>
