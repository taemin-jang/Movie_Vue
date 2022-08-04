<template>
  <div>
    <VideoView
      :display="videoShowValue"
      :movieId="videos"
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

                <a
                  href="https://www.youtube.com/watch?v=Q0CbN8sfihY"
                  class="play-video"
                >
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

                <a href="#" class="btn btn-main btn-effect">trailer</a>
                <a href="#" class="btn btn-main btn-effect">watch later</a>
                <a href="#" class="btn rate-movie"
                  ><i class="icon-heart"></i
                ></a>

                <div class="rating mt10">
                  <i class="fa fa-star"></i>
                  <i class="fa fa-star"></i>
                  <i class="fa fa-star"></i>
                  <i class="fa fa-star"></i>
                  <i class="fa fa-star-o"></i>
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
                  <h3 class="title">Storyline</h3>

                  <p>
                    {{ movieDetail.detail.overview }}
                  </p>
                </div>

                <!-- Media -->
                <div class="movie-media mt50">
                  <h3 class="title">Photos & Videos</h3>

                  <ul class="image-gallery isotope">
                    <li
                      class="element"
                      v-for="(item, i) in movieDetail.images"
                      :key="i"
                    >
                      <div v-if="i < 6">
                        <a
                          :href="`https://image.tmdb.org/t/p/original${movieDetail.images[i].file_path}`"
                        >
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
                          <div class="movie-box-1 upcoming-item">
                            <!-- Start of Poster -->
                            <div class="poster">
                              <img
                                :src="`https://img.youtube.com/vi/${items.key}/mqdefault.jpg`"
                                alt=""
                              />
                            </div>
                            <!-- End of Poster -->

                            <!-- Start of Buttons -->
                            <div class="buttons upcoming a">
                              <a
                                href="#"
                                class="play-video"
                                @click="videoShow(i)"
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
                <aside class="widget widget-movie-details">
                  <h3 class="title">Details</h3>

                  <ul>
                    <li>
                      <strong>개봉일: </strong
                      >{{ movieDetail.detail.release_date }}
                    </li>
                    <li>
                      <strong>감독: </strong
                      ><a href="#">{{
                        movieDetail.detail.production_companies[1].name
                      }}</a>
                    </li>
                    <li>
                      <strong>제작비: </strong
                      >{{ String(movieDetail.detail.budget).slice(0, 3) }}
                      million USD
                    </li>
                    <li>
                      <strong>제작한 나라: </strong
                      >{{
                        movieDetail.detail.production_companies[0]
                          .origin_country
                      }}
                    </li>
                    <li>
                      <strong>언어: </strong
                      >{{ movieDetail.detail.spoken_languages[0].name }}
                    </li>
                    <li>
                      <strong>제작사: </strong
                      ><a href="#">{{
                        movieDetail.detail.production_companies[0].name
                      }}</a>
                    </li>
                  </ul>
                </aside>
                <!-- End of Details Widget -->

                <!-- Start of Details Widget -->
                <aside class="widget widget-movie-cast">
                  <h3 class="title">Cast</h3>

                  <ul class="cast-wrapper">
                    <li v-for="(item, i) in 5" :key="i">
                      <a href="celebrity-detail.html">
                        <span class="circle-img">
                          <img :src="`${castImg(i)}`" alt="" />
                        </span>
                        <h6 class="name">{{ castName(i) }}</h6>
                      </a>
                    </li>
                  </ul>

                  <a
                    href="celebrities-list.html"
                    class="btn btn-main btn-effect mt20"
                    >view all</a
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
              <h2 class="title">People who liked this also liked...</h2>
            </div>
          </div>
          <!-- End of row -->

          <!-- Start of Latest Movies Slider -->
          <div class="owl-carousel recommended-slider mt20">
            <!-- === Start of Sliding Item 1 === -->
            <div class="item">
              <!-- Start of Movie Box -->
              <div
                class="movie-box-1"
                v-for="(recomItem, i) in movieDetail.recommendations"
                :key="i"
              >
                <!-- Start of Poster -->
                <div class="poster">
                  <img
                    :src="`https://image.tmdb.org/t/p/w300${recomItem[i].poster_path}`"
                    alt=""
                  />
                </div>
                <!-- End of Poster -->

                <!-- Start of Buttons -->
                <div class="buttons">
                  <a
                    href="https://www.youtube.com/watch?v=Q0CbN8sfihY"
                    class="play-video"
                  >
                    <i class="fa fa-play"></i>
                  </a>
                </div>
                <!-- End of Buttons -->

                <!-- Start of Movie Details -->
                <div class="movie-details">
                  <h4 class="movie-title">
                    <a href="movie-detail.html">Daredevil</a>
                  </h4>
                  <span class="released">19 Apr 2015</span>
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
                  <span>8.7 / 10</span>
                </div>
                <!-- End of Rating -->
              </div>
              <!-- End of Movie Box -->
            </div>
            <!-- === End of Sliding Item 1 === -->
          </div>
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
      <a href="#"></a>
    </div>
    <!-- ===== End of Back to Top Button ===== -->
  </div>
</template>

<script>
import HeaderView from "@/components/HeaderView.vue";
import FooterView from "@/components/FooterView.vue";
import VideoView from "@/components/Main/VideoView.vue";
import carousel from "vue-owl-carousel";
import axios from "axios";
export default {
  components: {
    HeaderView,
    FooterView,
    VideoView,
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
    };
  },
  methods: {
    genre(item, i) {
      return item[i].name;
    },
    releaseDate(i) {
      return this.movieDetail.detail.release_date.split("-")[i];
    },

    async videoShow(i) {
      this.videoShowValue = true;
      const video = await axios({
        method: "get",
        url: `https://api.themoviedb.org/3/movie/${this.$route.params.idx}/videos?api_key=0bb0b51dbb47771a2b73398672aac6cf&region=kr&language=ko`,
      });
      try {
        this.videos = video.data.results[i].key;
        console.log(this.videos);
      } catch (error) {
        this.videoShowValue = false;
        console.log("not find video");
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
  },

  computed: {},

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
    this.movieDetail.casts = cast.data.cast;
    console.log(this.movieDetail.casts);

    const recommendations = await axios({
      method: "get",
      url: `https://api.themoviedb.org/3/movie/${this.$route.params.idx}/recommendations?api_key=0bb0b51dbb47771a2b73398672aac6cf`,
    });
    this.movieDetail.recommendations = recommendations.data.results;
    console.log(this.movieDetail.recommendations);
  },
};
</script>

<style lang="scss" scoped></style>
