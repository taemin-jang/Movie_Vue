<template>
  <div class="wrapper">
    <HeaderView @show="modalShow" />
    <section
      class="page-header overlay-gradient"
      style="background: url(assets/images/posters/movie-collection.jpg)"
    >
      <div class="container">
        <div class="inner">
          <h2 class="title">Celebrities List</h2>
          <ol class="breadcrumb">
            <li><a href="index.html">Home</a></li>
            <li>Celebrities List</li>
          </ol>
        </div>
      </div>
    </section>
    <!-- =============== END OF PAGE HEADER =============== -->

    <!-- =============== START OF MAIN =============== -->
    <main class="ptb100">
      <div class="container">
        <!-- Start of Filters -->
        <div class="row mb50">
          <div class="col-md-6">
            <!-- Layout Switcher -->
            <div class="layout-switcher">
              <a class="list" @click="showLayout" :class="{ active: showList }"
                ><i class="fa fa-align-justify"></i
              ></a>
              <a class="grid" @click="showLayout" :class="{ active: showGrid }"
                ><i class="fa fa-th"></i
              ></a>
            </div>
          </div>
        </div>

        <!-- Start of Celebrities List -->
        <div class="list">
          <div class="row" :class="{ hidden: showGrid }">
            <div>
              <div v-for="(item, i) in filterCast" :key="i">
                <OtherCredit :item="item" />
              </div>
              <div class="layout-switcher buttonPage">
                <span
                  v-for="(num, i) in parseInt(casts.length / 6)"
                  :key="'page' + i"
                >
                  <a @click="chageCast(i)">{{ i + 1 }}</a>
                </span>
              </div>
            </div>
          </div>
        </div>

        <div class="grid">
          <div class="show" :class="{ hidden: showList }">
            <div class="row">
              <div>
                <div v-for="(item, i) in filterCast" :key="i">
                  <div v-if="i < 3">
                    <OtherCredit :item="item" />
                  </div>
                </div>
              </div>
              <div>
                <div v-for="(item, i) in filterCast" :key="i">
                  <div v-if="i < 6 && i >= 3">
                    <OtherCredit :item="item" />
                  </div>
                </div>
              </div>
            </div>
            <div class="layout-switcher buttonPage">
              <span
                v-for="(num, i) in parseInt(casts.length / 6)"
                :key="'page' + i"
              >
                <a @click="chageCast(i)">{{ i + 1 }}</a>
              </span>
            </div>
          </div>
        </div>
      </div>
    </main>
    <FooterView />
  </div>
</template>

<script>
import HeaderView from "@/components/HeaderView.vue";
import FooterView from "@/components/FooterView.vue";
import OtherCredit from "@/components/Credit/OtherCredit.vue";
import axios from "axios";
// import carousel from "vue-owl-carousel";
export default {
  components: {
    HeaderView,
    FooterView,
    OtherCredit,
    // carousel,
  },
  data() {
    return {
      casts: [],
      filterCast: [],
      castsDetail: [],
      modalShowValue: false,
      startNum: 0,
      endNum: 6,
      pageNum: 1,
      showList: true,
      showGrid: false,
    };
  },
  async mounted() {
    // const castDetail = await axios({
    //   method: "get",
    //   url: `https://api.themoviedb.org/3/credit/${this.casts[i].credit_id}?api_key=0bb0b51dbb47771a2b73398672aac6cf`,
    // });
    // this.castsDetail = castDetail.data;
    // console.log(this.castsDetail);
  },
  methods: {
    modalShow() {
      return (this.modalShowValue = true);
    },
    castImg(i) {
      try {
        return "https://image.tmdb.org/t/p/w300" + this.casts[i].profile_path;
      } catch (error) {
        return "#";
      }
    },
    castName(i) {
      try {
        return this.casts[i].name;
      } catch (error) {
        return "Non";
      }
    },
    chageCast(num) {
      this.startNum = 0;
      this.endNum = 6;
      console.log(num + "번 클릭");
      console.log(this.casts.length);
      if (num === 0) {
        console.log(this.startNum + "과 " + this.endNum);
        this.filterCast = this.casts.filter(
          (v, j) => j < this.endNum && j >= this.startNum
        );
        return this.filterCast;
      } else {
        for (let i = 1; i < this.casts.length / 6; i++) {
          if (num === i) {
            this.startNum = this.startNum + 6 * i;
            this.endNum = this.endNum + 6 * i;
            this.filterCast = this.casts.filter(
              (v, j) => j < this.endNum && j >= this.startNum
            );
            console.log(this.startNum + "과 " + this.endNum);
            return this.filterCast;
          }
        }
      }
    },
    showLayout(event) {
      console.log(event.target._prevClass);
      if (
        event.target._prevClass === "list active" ||
        event.target._prevClass === "list" ||
        event.target._prevClass === "fa fa-align-justify"
      ) {
        this.showList = true;
        this.showGrid = false;
      } else {
        this.showList = false;
        this.showGrid = true;
      }
    },
    async castText(i) {
      try {
        const castDetail = await axios({
          method: "get",
          url: `https://api.themoviedb.org/3/credit/${this.casts[i].credit_id}?api_key=0bb0b51dbb47771a2b73398672aac6cf`,
        });
        this.castsDetail = castDetail.data;
        console.log(this.castsDetail);
      } catch (error) {
        i === 0;
      }
    },
  },
  async created() {
    const cast = await axios({
      method: "get",
      url: `https://api.themoviedb.org/3/movie/${this.$route.params.idx}/credits?api_key=0bb0b51dbb47771a2b73398672aac6cf&region=kr&language=ko`,
    });
    this.casts = cast.data.cast.filter(
      (v, i) =>
        i < (cast.data.cast.length / 2 < 40 ? cast.data.cast.length : 35)
    );
    this.chageCast(0);
    // this.casts = cast.data.cast.filter(
    //   (v, i) => i < this.endNum && i > this.startNum
    // );
    console.log(this.casts);
  },
};
</script>

<style scoped>
.buttonPage {
  display: flex;
  justify-content: center;
}

.list div.row {
  display: block;
}

.list div.hidden {
  display: none;
}

.gird div.show {
  display: block;
}

.gird div.show + .grid div.row {
  flex-wrap: nowrap;
}

.grid div.hidden {
  display: none;
}
</style>
