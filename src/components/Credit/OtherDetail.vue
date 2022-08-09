<template>
  <div class="col-lg-8 col-12">
    <div class="celeb-details">
      <h3 class="title">{{ item.person?.name }}</h3>
      <span class="profession">{{ item.job }}</span>

      <!-- tab links -->
      <ul class="nav tab-links">
        <li class="nav-item">
          <a
            class="nav-link active"
            id="bio-tab"
            data-toggle="tab"
            href="#bio"
            aria-controls="bio"
            aria-expanded="false"
            >biography</a
          >
        </li>
        <li class="nav-item">
          <a
            class="nav-link"
            id="film-tab"
            data-toggle="tab"
            href="#filmography"
            aria-controls="filmography"
            aria-expanded="false"
            >filmography</a
          >
        </li>
      </ul>

      <!-- Tab Content -->
      <div class="tab-content mt70">
        <div
          class="tab-pane fade active show"
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
          class="tab-pane fade"
          id="filmography"
          role="tabpanel"
          aria-labelledby="film-tab"
          aria-expanded="false"
        >
          <ul class="film-list">
            <li><a href="#">Black Cage</a><span class="year">2017</span></li>
            <li><a href="#">Find Me </a><span class="year">2016</span></li>
            <li><a href="#">The 19th Life</a><span class="year">2016</span></li>
            <li><a href="#">Central Hit </a><span class="year">2016</span></li>
            <li><a href="#">Triple 7 </a><span class="year">2015</span></li>
            <li>
              <a href="#">Need for Space </a><span class="year">2014</span>
            </li>
            <li>
              <a href="#">Breaking Mad </a><span class="year">2008-2013</span>
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
  },
  async updated() {
    if (this.item.person) {
      const personDetail = await axios({
        method: "get",
        url: `https://api.themoviedb.org/3/person/${this.item.person.id}?api_key=0bb0b51dbb47771a2b73398672aac6cf`,
      });
      this.personDetails = personDetail.data;
    }
  },
};
</script>

<style lang="scss" scoped></style>
