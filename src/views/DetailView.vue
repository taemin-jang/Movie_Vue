<template>
  <div>
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
                    <li class="element">
                      <a
                        :href="`https://image.tmdb.org/t/p/original${movieDetail.images[0].file_path}`"
                      >
                        <img
                          :src="`https://image.tmdb.org/t/p/w300${movieDetail.images[0].file_path}`"
                          class="img-responsive"
                          alt=""
                      /></a>
                    </li>

                    <li class="element">
                      <a
                        :href="`https://image.tmdb.org/t/p/original${movieDetail.images[5].file_path}`"
                      >
                        <img
                          :src="`https://image.tmdb.org/t/p/w300${movieDetail.images[5].file_path}`"
                          class="img-responsive"
                          alt=""
                      /></a>
                    </li>

                    <li class="element">
                      <a href="assets/images/other/home2-bg.jpg">
                        <img
                          :src="require(`@/assets/images/other/home2-bg.jpg`)"
                          class="img-responsive"
                          alt=""
                        />
                      </a>
                    </li>

                    <li class="element">
                      <a href="assets/images/blog/bloglist-2.jpg">
                        <img
                          :src="require(`@/assets/images/blog/bloglist-2.jpg`)"
                          class="img-responsive"
                          alt=""
                        />
                      </a>
                    </li>

                    <li class="element">
                      <a href="assets/images/blog/bloglist-1.jpg">
                        <img
                          :src="require(`@/assets/images/blog/bloglist-1.jpg`)"
                          class="img-responsive"
                          alt=""
                        />
                      </a>
                    </li>

                    <li class="element">
                      <a href="assets/images/blog/bloglist-3.jpg">
                        <img
                          :src="require(`@/assets/images/blog/bloglist-3.jpg`)"
                          class="img-responsive"
                          alt=""
                        />
                      </a>
                    </li>

                    <li class="element">
                      <a href="assets/images/blog/bloglist-1.jpg">
                        <img
                          :src="require(`@/assets/images/blog/bloglist-1.jpg`)"
                          class="img-responsive"
                          alt=""
                        />
                      </a>
                    </li>

                    <li class="element">
                      <a href="assets/images/other/landscape.jpg">
                        <img
                          :src="require(`@/assets/images/other/landscape.jpg`)"
                          class="img-responsive"
                          alt=""
                        />
                      </a>
                    </li>

                    <li class="element">
                      <a href="assets/images/other/home2-bg.jpg">
                        <img
                          :src="require(`@/assets/images/other/home2-bg.jpg`)"
                          class="img-responsive"
                          alt=""
                        />
                      </a>
                    </li>
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
                    <li>
                      <a href="celebrity-detail.html">
                        <span class="circle-img">
                          <img
                            :src="
                              require(`@/assets/images/celebrities/celebrity1.jpg`)
                            "
                            alt=""
                          />
                        </span>
                        <h6 class="name">Bryan Doe</h6>
                      </a>
                    </li>

                    <li>
                      <a href="celebrity-detail.html">
                        <span class="circle-img">
                          <img
                            :src="
                              require(`@/assets/images/celebrities/celebrity2.jpg`)
                            "
                            alt=""
                          />
                        </span>
                        <h6 class="name">Baron Saul</h6>
                      </a>
                    </li>

                    <li>
                      <a href="celebrity-detail.html">
                        <span class="circle-img">
                          <img
                            :src="
                              require(`@/assets/images/celebrities/celebrity3.jpg`)
                            "
                            alt=""
                          />
                        </span>
                        <h6 class="name">Ewan Actor</h6>
                      </a>
                    </li>

                    <li>
                      <a href="celebrity-detail.html">
                        <span class="circle-img">
                          <img
                            :src="
                              require(`@/assets/images/celebrities/celebrity4.jpg`)
                            "
                            alt=""
                          />
                        </span>
                        <h6 class="name">Nicole Beet</h6>
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
              <div class="movie-box-1">
                <!-- Start of Poster -->
                <div class="poster">
                  <img
                    :src="require(`@/assets/images/posters/poster-5.jpg`)"
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

            <!-- === Start of Sliding Item 2 === -->
            <div class="item">
              <!-- Start of Movie Box -->
              <div class="movie-box-1">
                <!-- Start of Poster -->
                <div class="poster">
                  <img
                    :src="require(`@/assets/images/posters/poster-6.jpg`)"
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
                    <a href="movie-detail.html">Stranger Things</a>
                  </h4>
                  <span class="released">15 Jul 2016</span>
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
                  <span>9 / 10</span>
                </div>
                <!-- End of Rating -->
              </div>
              <!-- End of Movie Box -->
            </div>
            <!-- === End of Sliding Item 2 === -->

            <!-- === Start of Sliding Item 3 === -->
            <div class="item">
              <!-- Start of Movie Box -->
              <div class="movie-box-1">
                <!-- Start of Poster -->
                <div class="poster">
                  <img
                    :src="require(`@/assets/images/posters/poster-7.jpg`)"
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
                    <a href="movie-detail.html">Luke Cage</a>
                  </h4>
                  <span class="released">30 Sep 2016</span>
                </div>
                <!-- End of Movie Details -->

                <!-- Start of Rating -->
                <div class="stars">
                  <div class="rating">
                    <i class="fa fa-star"></i>
                    <i class="fa fa-star"></i>
                    <i class="fa fa-star"></i>
                    <i class="fa fa-star-half-o"></i>
                    <i class="fa fa-star-o"></i>
                  </div>
                  <span>7.6 / 10</span>
                </div>
                <!-- End of Rating -->
              </div>
              <!-- End of Movie Box -->
            </div>
            <!-- === End of Sliding Item 3 === -->

            <!-- === Start of Sliding Item 4 === -->
            <div class="item">
              <!-- Start of Movie Box -->
              <div class="movie-box-1">
                <!-- Start of Poster -->
                <div class="poster">
                  <img
                    :src="require(`@/assets/images/posters/poster-8.jpg`)"
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
                    <a href="movie-detail.html">The Flash</a>
                  </h4>
                  <span class="released">7 Oct 2014</span>
                </div>
                <!-- End of Movie Details -->

                <!-- Start of Rating -->
                <div class="stars">
                  <div class="rating">
                    <i class="fa fa-star"></i>
                    <i class="fa fa-star"></i>
                    <i class="fa fa-star"></i>
                    <i class="fa fa-star"></i>
                    <i class="fa fa-star-o"></i>
                  </div>
                  <span>8 / 10</span>
                </div>
                <!-- End of Rating -->
              </div>
              <!-- End of Movie Box -->
            </div>
            <!-- === End of Sliding Item 4 === -->

            <!-- === Start of Sliding Item 5 === -->
            <div class="item">
              <!-- Start of Movie Box -->
              <div class="movie-box-1">
                <!-- Start of Poster -->
                <div class="poster">
                  <img
                    :src="require(`@/assets/images/posters/poster-5.jpg`)"
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
            <!-- === End of Sliding Item 5 === -->

            <!-- === Start of Sliding Item 6 === -->
            <div class="item">
              <!-- Start of Movie Box -->
              <div class="movie-box-1">
                <!-- Start of Poster -->
                <div class="poster">
                  <img
                    :src="require(`@/assets/images/posters/poster-6.jpg`)"
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
                    <a href="movie-detail.html">Stranger Things</a>
                  </h4>
                  <span class="released">15 Jul 2016</span>
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
                  <span>9 / 10</span>
                </div>
                <!-- End of Rating -->
              </div>
              <!-- End of Movie Box -->
            </div>
            <!-- === End of Sliding Item 6 === -->
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

    <!-- =============== START OF LOGIN & REGISTER POPUP =============== -->
    <div
      id="login-register-popup"
      class="small-dialog zoom-anim-dialog mfp-hide"
    >
      <!-- ===== Start of Signin wrapper ===== -->
      <div class="signin-wrapper">
        <div class="small-dialog-headline">
          <h4 class="text-center">Sign in</h4>
        </div>

        <div class="small-dialog-content">
          <!-- Start of Login form -->
          <form id="cariera_login" method="post">
            <p class="status"></p>

            <div class="form-group">
              <label for="username">Username or Email *</label>
              <input
                type="text"
                class="form-control"
                id="username"
                name="username"
                placeholder="Your Username or Email *"
              />
            </div>

            <div class="form-group">
              <label for="password">Password *</label>
              <input
                type="password"
                class="form-control"
                id="password"
                name="password"
                placeholder="Your Password *"
              />
            </div>

            <div class="form-group">
              <div class="checkbox pad-bottom-10">
                <input
                  id="check1"
                  type="checkbox"
                  name="remember"
                  value="yes"
                />
                <label for="check1">Keep me signed in</label>
              </div>
            </div>

            <div class="form-group">
              <input
                type="submit"
                value="Sign in"
                class="btn btn-main btn-effect nomargin"
              />
            </div>
          </form>
          <!-- End of Login form -->

          <div class="bottom-links">
            <span>
              Not a member?
              <a class="signUpClick">Sign up</a>
            </span>
            <a class="forgetPasswordClick pull-right">Forgot Password</a>
          </div>
        </div>
      </div>
      <!-- ===== End of Signin wrapper ===== -->

      <!-- ===== Start of Signup wrapper ===== -->
      <div class="signup-wrapper">
        <div class="small-dialog-headline">
          <h4 class="text-center">Sign Up</h4>
        </div>

        <div class="small-dialog-content">
          <!-- Start of Registration form -->
          <form id="cariera_registration" action="#" method="POST">
            <p class="status"></p>

            <div class="form-group">
              <label for="movify_user_login">Username</label>
              <input
                name="movify_user_login"
                id="movify_user_login"
                class="form-control"
                type="text"
              />
            </div>

            <div class="form-group">
              <label for="movify_user_email">Email</label>
              <input
                name="movify_user_email"
                id="movify_user_email"
                class="form-control"
                type="email"
              />
            </div>

            <div class="form-group">
              <label for="password">Password</label>
              <input
                name="movify_user_pass"
                id="movify_password"
                class="form-control"
                type="password"
              />
            </div>

            <div class="form-group">
              <input
                type="submit"
                class="btn btn-main btn-effect nomargin"
                value="Register"
              />
            </div>
          </form>
          <!-- End of Registration form -->

          <div class="bottom-links">
            <span>
              Already have an account?
              <a class="signInClick">Sign in</a>
            </span>

            <a class="forgetPasswordClick pull-right">Forgot Password</a>
          </div>
        </div>
        <!-- .small-dialog-content -->
      </div>
      <!-- ===== End of Signup wrapper ===== -->

      <!-- ===== Start of Forget Password wrapper ===== -->
      <div class="forgetpassword-wrapper">
        <div class="small-dialog-headline">
          <h4 class="text-center">Forgotten Password</h4>
        </div>

        <div class="small-dialog-content">
          <!-- Start of Forger Password form -->
          <form id="forget_pass_form" action="#" method="post">
            <p class="status"></p>

            <div class="form-group">
              <label for="password">Email Address *</label>
              <input
                type="email"
                name="user_login"
                class="form-control"
                id="email3"
                placeholder="Email Address *"
              />
            </div>

            <div class="form-group">
              <input
                type="submit"
                name="submit"
                value="Get New Password"
                class="btn btn-main btn-effect nomargin"
              />
            </div>
          </form>
          <!-- End of Forger Password form -->

          <div class="bottom-links">
            <a class="cancelClick">Cancel</a>
          </div>
        </div>
        <!-- .small-dialog-content -->
      </div>
      <!-- ===== End of Forget Password wrapper ===== -->
    </div>
    <!-- =============== END OF LOGIN & REGISTER POPUP =============== -->

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
import axios from "axios";
export default {
  components: {
    HeaderView,
    FooterView,
  },
  data() {
    return {
      movieDetail: {
        detail: [],
        images: [],
      },
    };
  },
  methods: {
    genre(item, i) {
      return item[i].name;
    },
    releaseDate(i) {
      return this.movieDetail.detail.release_date.split("-")[i];
    },
  },
  computed: {},
  async created() {
    const detail = await axios({
      method: "get",
      url: `https://api.themoviedb.org/3/movie/${this.$route.params.idx}?api_key=0bb0b51dbb47771a2b73398672aac6cf&region=kr&language=ko`,
    });
    this.movieDetail.detail = detail.data;
    console.log(this.movieDetail.detail.spoken_languages);
    console.log(this.$route.params.idx);

    const images = await axios({
      method: "get",
      url: `https://api.themoviedb.org/3/movie/${this.$route.params.idx}/images?api_key=0bb0b51dbb47771a2b73398672aac6cf&region=kr&language=ko`,
    });
    this.movieDetail.images = images.data.posters;
    console.log(this.movieDetail.images);
  },
};
</script>

<style lang="scss" scoped></style>
