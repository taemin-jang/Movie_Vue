<template>
  <div>
    <HeaderView />
    <!-- =============== START OF MOVIE DETAIL INTRO =============== -->
    <section
      class="celeb-detail-intro overlay-gradient ptb100"
      :style="{
        background:
          'url(' +
          `https://image.tmdb.org/t/p/original/${credits.media?.backdrop_path})`,
      }"
    ></section>
    <!-- =============== END OF MOVIE DETAIL INTRO =============== -->

    <!-- =============== START OF CELEBRITY DETAIL =============== -->
    <section class="celeb-detail pb100">
      <div class="container">
        <div class="row">
          <div class="col-lg-4 col-12">
            <div class="celeb-img">
              <img :src="`${getImg()}`" alt="" />
            </div>
          </div>

          <OtherDetail :item="credits" />
        </div>
      </div>
    </section>
    <FooterView />
  </div>
</template>

<script>
import HeaderView from "@/components/HeaderView.vue";
import FooterView from "@/components/FooterView.vue";
import OtherDetail from "@/components/Credit/OtherDetail.vue";
import axios from "axios";
export default {
  components: {
    HeaderView,
    FooterView,
    OtherDetail,
  },
  data() {
    return {
      credits: [],
      personId: 0,
    };
  },
  methods: {
    getImg() {
      if (this.credits.person?.profile_path !== null) {
        return `https://image.tmdb.org/t/p/w300/${this.credits.person?.profile_path}`;
      } else {
        //이미지 null인경우 빈 이미지 추가
        return "https://dummyimage.com/300x450/d6d6d6/ffffff.png&text=Not+Image";
      }
    },
  },
  async created() {
    const credit = await axios({
      method: "get",
      url: `https://api.themoviedb.org/3/credit/${this.$route.params.idx}?api_key=0bb0b51dbb47771a2b73398672aac6cf&language=ko`,
    });
    this.credits = credit.data;

    // this.personId = this.credits.person.id;
    // console.log(this.personId);
  },
};
</script>

<style lang="scss" scoped></style>
