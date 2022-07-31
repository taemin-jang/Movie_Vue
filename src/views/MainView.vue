<template>
  <div>
    <VideoView
      :display="videoShowValue"
      :movieId="videos"
      @close="videoClose"
    />
    <!-- =============== START OF PRELOADER =============== -->
    <!-- <div class="loading">
      <div class="loading-inner">
        <div class="loading-effect">
          <div class="object"></div>
        </div>
      </div>
    </div> -->
    <!-- =============== END OF PRELOADER =============== -->
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
      <SliderView />
      <!-- =============== START OF SLIDER REVOLUTION SECTION =============== -->

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
                          href="#"
                          data-original-title="Rate"
                          data-toggle="tooltip"
                          data-placement="bottom"
                          class="like"
                        >
                          <i class="icon-heart"></i>
                        </a>

                        <a
                          href="#"
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
                          <i class="fa fa-star"></i>
                          <i class="fa fa-star"></i>
                          <i class="fa fa-star"></i>
                          <i class="fa fa-star"></i>
                          <i class="fa fa-star-o"></i>
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
                          >details</router-link
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
          <div class="row">
            <!-- 1st Count up item -->
            <div class="col-md-4 col-sm-12">
              <span class="counter-item" data-from="0" data-to="964">0</span>
              <h4>Movies</h4>
            </div>

            <!-- 2nd Count up item -->
            <div class="col-md-4 col-sm-12">
              <span class="counter-item" data-from="0" data-to="743">0</span>
              <h4>TV Shows</h4>
            </div>

            <!-- 3rd Count up item -->
            <div class="col-md-4 col-sm-12">
              <span class="counter-item" data-from="0" data-to="1207">0</span>
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
              <h2 class="title">Latest Movies & TV Shows</h2>
              <h6 class="subtitle">
                Lorem ipsum dolor sit amet, consectetuer adipiscing elit, sed
                diam nonummy consectetuer adipiscing.
              </h6>
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
              <div class="movie-box-3" style="height: 685px">
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
                          href="#"
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

                      <p>
                        {{ items.overview }}
                      </p>

                      <a
                        href="movie-detail.html"
                        class="btn btn-main btn-effect"
                        style=""
                        >details</a
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
      <section
        class="upcoming-movies parallax ptb100"
        data-background="../assets/images/posters/movie-collection.jpg"
        data-color="#3e4555"
        data-color-opacity="0.95"
      >
        <div class="container">
          <!-- Start of row -->
          <div class="row justify-content-center">
            <div class="col-md-7 text-center">
              <h2 class="title text-white">Upcoming Movies & TV Shows</h2>
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
                      href="#"
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
                      <a href="movie-detail.html">{{
                        upComingRand(0, "title")
                      }}</a>
                    </h4>
                    <span class="released"
                      >Release Date:
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
                      href="#"
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
                      <a href="movie-detail.html">{{
                        upComingRand(1, "title")
                      }}</a>
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
                      href="#"
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
                      <a href="movie-detail.html">{{
                        upComingRand(2, "title")
                      }}</a>
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

      <!-- =============== END OF BECOME PREMIUM SECTION =============== -->
      <section class="become-premium3 ptb100">
        <div class="container">
          <!-- Start of row -->
          <div class="row justify-content-center">
            <div class="col-md-7 text-center">
              <h2 class="title">Become a Premium Member</h2>
              <h6 class="subtitle">
                Lorem ipsum dolor sit amet, consectetuer adipiscing elit.
              </h6>
            </div>
          </div>
          <!-- End of row -->

          <!-- Start of row -->
          <div class="row mt80">
            <div class="col-md-12">
              <!-- Start of Pricing Table -->
              <div class="pricing-table-2">
                <!-- Pricing Plan 1 -->
                <div class="plan">
                  <!-- Price -->
                  <div class="plan-price">
                    <h3>Basic</h3>
                    <span class="value">Free</span>
                    <span class="period"
                      >Try Movify for FREE for the first 7 days, you can upgrade
                      anytime.</span
                    >
                  </div>

                  <!-- Features -->
                  <div class="plan-features">
                    <ul>
                      <li>7 days</li>
                      <li>720p Resolution</li>
                      <li>Desktop Only</li>
                      <li>Limited Support</li>
                    </ul>
                    <a class="btn btn-main btn-effect mt30" href="#"
                      >Get Started</a
                    >
                  </div>
                </div>

                <!-- Featured - Pricing Plan 2 -->
                <div class="plan featured">
                  <!-- Price -->
                  <div class="plan-price">
                    <h3>Premium</h3>
                    <span class="value">$19</span>
                    <span class="period"
                      >Most wanted subscription package by our Movifiers.</span
                    >
                  </div>

                  <!-- Features -->
                  <div class="plan-features">
                    <ul>
                      <li>1 Month</li>
                      <li>Full HD</li>
                      <li>Lifetime Availability</li>
                      <li>TV & Desktop</li>
                      <li>24/7 Support</li>
                    </ul>
                    <a class="btn btn-main btn-effect mt30" href="#"
                      >Get Started</a
                    >
                  </div>
                </div>

                <!-- Pricing Plan 3 -->
                <div class="plan">
                  <!-- Price -->
                  <div class="plan-price">
                    <h3>Cinematic</h3>
                    <span class="value">$39</span>
                    <span class="period"
                      >Watch your favorite movies anywhere and anytime.</span
                    >
                  </div>

                  <!-- Features -->
                  <div class="plan-features">
                    <ul>
                      <li>2 Months</li>
                      <li>Ultra HD</li>
                      <li>Any Device</li>
                      <li>24/7 Support</li>
                    </ul>
                    <a class="btn btn-main btn-effect mt30" href="#"
                      >Get Started</a
                    >
                  </div>
                </div>
              </div>
              <!-- End of Pricing Table -->
            </div>
          </div>
          <!-- End of row -->
        </div>
      </section>
      <!-- =============== END OF BECOME PREMIUM SECTION =============== -->

      <!-- =============== END OF BLOG SECTION =============== -->
      <section class="blog bg-light ptb100">
        <div class="container">
          <!-- Start of row -->
          <div class="row justify-content-center">
            <div class="col-md-7 text-center">
              <h2 class="title">Latest News</h2>
              <h6 class="subtitle">
                Lorem ipsum dolor sit amet, consectetuer adipiscing elit, sed
                diam nonummy consectetuer adipiscing.
              </h6>
            </div>
          </div>
          <!-- End of row -->

          <!-- Start of row -->
          <div class="row mt50">
            <!-- 1st Blog Item -->
            <div class="col-md-4">
              <div class="bloglist-post-holder shadow-hover">
                <!-- Blog Post Thumbnail -->
                <a
                  href="blog-post-detail.html"
                  class="bloglist-thumb-link hover-link"
                >
                  <div
                    class="bloglist-post-thumbnail"
                    style="
                      background: require(
                        `../assets/images/blog/bloglist-1.jpg`
                      );
                    "
                  ></div>
                </a>

                <!-- Blog Post Text Wrapper -->
                <div class="bloglist-text-wrapper">
                  <!-- Author Avatar -->
                  <span class="circle-img bloglist-avatar">
                    <img
                      src="../assets/images/user.png"
                      width="50"
                      height="50"
                      alt="author img"
                    />
                  </span>

                  <h4 class="bloglist-title">
                    <a href="blog-post-detail.html">Top 10 Action Movies</a>
                  </h4>

                  <div class="bloglist-meta">
                    <i class="fa fa-calendar"></i> 01/02/2018
                  </div>

                  <div class="bloglist-excerpt">
                    <p>
                      Sed ut perspiciatis unde omnis iste natus error sit
                      voluptatem accusantium doloremque laudantium, totam rem
                      aperiam, eaque ipsa quae ab illo inventore veritatis...
                    </p>
                    <a href="#" class="btn btn-main btn-effect">read more</a>
                  </div>
                </div>
              </div>
            </div>

            <!-- 2nd Blog Item -->
            <div class="col-md-4">
              <div class="bloglist-post-holder shadow-hover">
                <!-- Blog Post Thumbnail -->
                <a
                  href="blog-post-detail.html"
                  class="bloglist-thumb-link hover-link"
                >
                  <div
                    class="bloglist-post-thumbnail"
                    style="
                      background: require(
                        `../assets/images/blog/bloglist-2.jpg`
                      );
                    "
                  ></div>
                </a>

                <!-- Blog Post Text Wrapper -->
                <div class="bloglist-text-wrapper">
                  <!-- Author Avatar -->
                  <span class="circle-img bloglist-avatar">
                    <img
                      src="../assets/images/user.png"
                      width="50"
                      height="50"
                      alt="author img"
                    />
                  </span>

                  <h4 class="bloglist-title">
                    <a href="blog-post-detail.html">Oscar Awards</a>
                  </h4>

                  <div class="bloglist-meta">
                    <i class="fa fa-calendar"></i> 01/02/2018
                  </div>

                  <div class="bloglist-excerpt">
                    <p>
                      Sed ut perspiciatis unde omnis iste natus error sit
                      voluptatem accusantium doloremque laudantium, totam rem
                      aperiam, eaque ipsa quae ab illo inventore veritatis...
                    </p>
                    <a href="#" class="btn btn-main btn-effect">read more</a>
                  </div>
                </div>
              </div>
            </div>

            <!-- 3rd Blog Item -->
            <div class="col-md-4">
              <div class="bloglist-post-holder shadow-hover">
                <!-- Blog Post Thumbnail -->
                <a
                  href="blog-post-detail.html"
                  class="bloglist-thumb-link hover-link"
                >
                  <div
                    class="bloglist-post-thumbnail"
                    style="
                      background: require(
                        `../assets/images/blog/bloglist-3.jpg`
                      );
                    "
                  ></div>
                </a>

                <!-- Blog Post Text Wrapper -->
                <div class="bloglist-text-wrapper">
                  <!-- Author Avatar -->
                  <span class="circle-img bloglist-avatar">
                    <img
                      src="../assets/images/user.png"
                      width="50"
                      height="50"
                      alt="author img"
                    />
                  </span>

                  <h4 class="bloglist-title">
                    <a href="blog-post-detail.html">Top Upcoming Movies</a>
                  </h4>

                  <div class="bloglist-meta">
                    <i class="fa fa-calendar"></i> 01/02/2018
                  </div>

                  <div class="bloglist-excerpt">
                    <p>
                      Sed ut perspiciatis unde omnis iste natus error sit
                      voluptatem accusantium doloremque laudantium, totam rem
                      aperiam, eaque ipsa quae ab illo inventore veritatis...
                    </p>
                    <a href="#" class="btn btn-main btn-effect">read more</a>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <!-- End of row -->
        </div>
      </section>
      <!-- =============== END OF BLOG SECTION =============== -->

      <!-- =============== END OF SUBSCRIBE SECTION =============== -->
      <section class="subscribe bg-light2 ptb100">
        <div class="container">
          <!-- Start of row -->
          <div class="row">
            <div class="col-md-6 col-12">
              <div class="img-box overlay-gradient mr30">
                <img
                  src="../assets/images/other/landscape.jpg"
                  alt=""
                  class="img-resonsive img-shadow"
                />
              </div>
            </div>

            <div class="col-md-6 col-12 mt50">
              <h2 class="title">Join Movify Now!</h2>
              <h6 class="subtitle">
                Lorem ipsum dolor sit amet, consectetuer adipiscing elit, sed
                diam nonummy consectetuer adipiscing.
              </h6>

              <!-- Subscribe Form -->
              <form action="#" class="mailchimp mt50" novalidate>
                <!-- Form -->
                <div class="form-group">
                  <div class="input-group">
                    <input
                      type="email"
                      name="EMAIL"
                      class="form-control"
                      id="mc-email"
                      placeholder="Your Email"
                      autocomplete="off"
                    />
                    <label for="mc-email"></label>
                    <button type="submit" class="btn btn-main btn-effect">
                      Subscribe
                    </button>
                  </div>
                </div>
              </form>
            </div>
          </div>
          <!-- End of row -->
        </div>
      </section>
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
            // v-if문 걸어논 곳은 dom 접근이 안되나여??
            //document.querySelector(".poster img").style.height = "31.7vh";
            //console.log(document.querySelector(".plz .poster"));
            return this.upComing.upComing[this.i + e].poster_path;
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
        console.log("not find video");
      }
    },

    videoClose() {
      return (this.videoShowValue = false);
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
  },
  computed: {},
};
</script>

<style lang="scss" scoped></style>
