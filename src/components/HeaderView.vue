<template>
  <div>
    <header class="header header-fixed header-transparent text-white">
      <div class="container-fluid">
        <!-- ====== Start of Navbar ====== -->
        <nav class="navbar navbar-expand-lg">
          <router-link class="navbar-brand" :to="`/`">
            <!-- INSERT YOUR LOGO HERE -->
            <img
              src="../assets/images/logo.svg"
              alt="logo"
              width="150"
              class="logo"
            />
            <!-- INSERT YOUR WHITE LOGO HERE -->
            <img
              src="../assets/images/logo-white.svg"
              alt="white logo"
              width="150"
              class="logo-white"
            />
          </router-link>

          <!-- Login Button on Responsive -->
          <a
            href="#login-register-popup"
            class="login-mobile-btn popup-with-zoom-anim"
            ><i class="icon-user"></i
          ></a>

          <button
            id="mobile-nav-toggler"
            class="hamburger hamburger--collapse"
            type="button"
          >
            <span class="hamburger-box">
              <span class="hamburger-inner"></span>
            </span>
          </button>

          <!-- ====== Start of #main-nav ====== -->
          <div class="navbar-collapse" id="main-nav">
            <!-- ====== Start of Main Menu ====== -->
            <ul class="navbar-nav mx-auto" id="main-menu">
              <!-- Menu Item -->
              <li class="nav-item dropdown">
                <a
                  class="nav-link dropdown-toggle"
                  href="javascript:void(0)"
                  data-toggle="dropdown"
                  aria-haspopup="true"
                  aria-expanded="false"
                  >영화</a
                >

                <!-- Dropdown Menu -->
                <ul class="dropdown-menu">
                  <!-- Menu Item -->
                  <li>
                    <a class="dropdown-item" href="blog-list.html"
                      >현재 상영중인 영화</a
                    >
                  </li>

                  <!-- Menu Item -->
                  <li>
                    <a class="dropdown-item" href="blog-list-fullwidth.html"
                      >개봉 예정 영화</a
                    >
                  </li>

                  <!-- Menu Item -->
                  <li>
                    <a class="dropdown-item" href="blog-post-detail.html"
                      >인기 영화</a
                    >
                  </li>
                </ul>
              </li>

              <!-- Menu Item -->
              <li class="nav-item dropdown">
                <a
                  class="nav-link dropdown-toggle"
                  href="javascript:void(0)"
                  data-toggle="dropdown"
                  aria-haspopup="true"
                  aria-expanded="false"
                  >출연자</a
                >
              </li>
            </ul>
            <!-- ====== End of Main Menu ====== -->

            <!-- ====== Start of Extra Nav ====== -->
            <ul class="navbar-nav extra-nav">
              <!-- Menu Item -->
              <li class="nav-item">
                <a
                  class="nav-link toggle-search"
                  href="javascript:void(0)"
                  id="general-search-wrapper"
                  @click="openSearch"
                >
                  <i class="fa fa-search"></i>
                </a>
              </li>

              <!-- Menu Item -->
              <li class="nav-item notification-wrapper">
                <a class="nav-link notification" href="javascript:void(0)">
                  <i class="fa fa-globe"></i>
                  <span class="notification-count">2</span>
                </a>
              </li>

              <!-- Menu Item -->
              <li class="nav-item m-auto">
                <a
                  href="#login-register-popup"
                  class="btn btn-main btn-effect login-btn popup-with-zoom-anim"
                  @click="login"
                >
                  <i class="icon-user"></i>login
                </a>
              </li>
            </ul>
            <!-- ====== End of Extra Nav ====== -->
          </div>
          <!-- ====== End of #main-nav ====== -->
        </nav>
        <!-- ====== End of Navbar ====== -->
      </div>
      <div class="general-search-wrapper" :class="{ open: openSearchValue }">
        <form class="general-search" :action="`/search/${searchInput}`">
          <input
            v-model="searchInput"
            type="text"
            placeholder="Type and hit enter..."
          />

          <span
            id="general-search-close"
            class="ti-close toggle-search"
            @click="openSearch"
          ></span>
        </form>
      </div>
    </header>
    <!-- =============== END OF HEADER NAVIGATION =============== -->
  </div>
</template>

<script>
export default {
  data() {
    return {
      openSearchValue: false,
      searchInput: "",
    };
  },
  methods: {
    login(e) {
      e.preventDefault();
      this.$emit("show");
    },
    openSearch(event) {
      event.preventDefault();
      console.log(this.searchInput);
      if (event.target._prevClass === "fa fa-search") {
        this.openSearchValue = true;
      } else {
        this.$emit("searchMovie");
        this.openSearchValue = false;
      }
    },
  },
};
</script>

<style scoped></style>
