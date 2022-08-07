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
              <a href="celebrities-list.html" class="list active"
                ><i class="fa fa-align-justify"></i
              ></a>
              <a href="celebrities-grid.html" class="grid"
                ><i class="fa fa-th"></i
              ></a>
            </div>
          </div>

          <div class="col-md-6">
            <!-- Sort by -->
            <div class="sort-by">
              <div class="sort-by-select">
                <select class="chosen-select-no-single">
                  <option>Default Order</option>
                  <option>Featured</option>
                  <option>Top Viewed</option>
                  <option>Top Rated</option>
                  <option>Newest</option>
                  <option>Oldest</option>
                </select>
              </div>
            </div>
            <!-- Sort by / End -->
          </div>
        </div>
        <!-- End of Filters -->

        <!-- Start of Celebrities List -->
        <div class="row">
          <!-- Celebrity List Item -->
          <!-- <div v-for="(num, i) in casts.length" :key="i">
            <CreditDetail :creditId="casts[i].credit_id" />
          </div> -->
          <div v-for="(item, i) in casts" :key="i">
            <OtherCredit :item="item" />
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
export default {
  components: {
    HeaderView,
    FooterView,
    OtherCredit,
  },
  data() {
    return {
      casts: [],
      castsDetail: [],
      modalShowValue: false,
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
    this.casts = cast.data.cast.filter((v, i) => i < 6);
    console.log(this.casts);
  },
};
</script>

<style lang="scss" scoped></style>
