<template>
  <div class="col-lg-8 col-12">
    <div class="celeb-details">
      <h3 class="title">{{ item.person?.name }}</h3>
      <span class="profession">{{ item.job }}</span>

      <!-- tab links -->
      <ul class="nav tab-links">
        <li class="nav-item">
          <a
            class="nav-link show"
            :class="{ active: showBio }"
            @click="showTab"
            id="bio-tab"
            data-toggle="tab"
            href="javascript:void(0)"
            aria-controls="bio"
            aria-expanded="false"
            >biography</a
          >
        </li>
        <li class="nav-item">
          <a
            class="nav-link show"
            :class="{ active: !showBio }"
            @click="showTab"
            id="film-tab"
            data-toggle="tab"
            href="javascript:void(0)"
            aria-controls="filmography"
            aria-expanded="false"
            >filmography</a
          >
        </li>
      </ul>

      <!-- Tab Content -->
      <div class="tab-content mt70">
        <div
          class="tab-pane fade show"
          :class="{ active: showBio }"
          id="bio"
          role="tabpanel"
          aria-labelledby="bio-tab"
          aria-expanded="false"
        >
          <div class="bio-description">
            <p>{{ personDetails.biography }}</p>
          </div>

          <div class="bio-details">
            <ul class="bio-wrapper">
              <li>
                <h6>생일:</h6>
                {{ personDetails.birthday }}
              </li>
              <li>
                <h6>성별:</h6>
                {{ isGender() }}
              </li>
              <li>
                <h6>태어난 곳:</h6>
                {{ personDetails.place_of_birth }}
              </li>
            </ul>
          </div>

          <div class="clearfix"></div>
        </div>

        <div
          class="tab-pane fade show"
          :class="{ active: !showBio }"
          id="filmography"
          role="tabpanel"
          aria-labelledby="film-tab"
          aria-expanded="false"
        >
          <ul class="film-list">
            <li v-for="(item, i) in discoverMovies" :key="'discover' + i">
              <router-link :to="`/detail/${item.id}`">{{
                item.title
              }}</router-link
              ><span class="year">{{ item.release_date.slice(0, 4) }}</span>
            </li>
          </ul>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  data() {
    return {
      personDetails: [],
      discoverMovies: [],
      showBio: true,
    };
  },
  props: ["item"],
  mounted() {},
  methods: {
    isGender() {
      if (this.personDetails.gender === 1) {
        return "여성";
      } else if (this.personDetails.gender === 2) {
        return "남성";
      }
    },
    showTab(event) {
      console.log(event.target.id);

      if (event.target.id === "bio-tab") {
        this.showBio = true;
      } else {
        this.showBio = false;
      }
    },
  },
  async updated() {
    if (this.item.person) {
      const personDetail = await axios({
        method: "get",
        url: `https://api.themoviedb.org/3/person/${this.item.person.id}?api_key=0bb0b51dbb47771a2b73398672aac6cf`,
      });
      this.personDetails = personDetail.data;

      const discoverMovie = await axios({
        method: "get",
        url: `https://api.themoviedb.org/3/discover/movie?api_key=3d6c850fedd64a507e51cfb2335f305c&with_cast=${this.item.person.id}&sort_by=release_date.desc&language=ko`,
      });
      this.discoverMovies = discoverMovie.data.results.filter((v, i) => i < 10);
    }
  },

  async created() {},
};
</script>

<style scoped>
.tab-pane.fade {
  display: none;
}

.tab-pane.fade.active {
  display: block;
}
</style>
