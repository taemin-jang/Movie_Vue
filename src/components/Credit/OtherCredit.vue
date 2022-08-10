<template>
  <div class="col-md-12 col-sm-12">
    <div class="celebrity-list-1">
      <div class="celeb-container">
        <!-- Celebrity Image -->
        <div class="celebrity-image">
          <router-link :to="`/credit/detail/${item.credit_id}`">
            <img :src="`${getImg()}`" alt="" />
          </router-link>
        </div>

        <!-- Celebrity Content -->
        <div class="celebrity-content">
          <div class="inner">
            <h3 class="title">
              <router-link :to="`/credit/detail/${item.credit_id}`">{{
                item.name
              }}</router-link>
            </h3>
            <p class="line-clamp">
              {{ credits.overview }}
            </p>
          </div>
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
      credits: [],
      controlItem: [],
    };
  },
  props: ["item"],
  mounted() {},
  methods: {
    getImg() {
      if (this.item.profile_path !== null) {
        return `https://image.tmdb.org/t/p/w300/${this.item.profile_path}`;
      } else {
        //이미지 null인경우 빈 이미지 추가
        return "https://dummyimage.com/300x450/d6d6d6/ffffff.png&text=Not+Image";
      }
    },
  },
  async created() {
    console.log(this.item);
    const credit = await axios({
      method: "get",
      url: `https://api.themoviedb.org/3/credit/${this.item.credit_id}?api_key=0bb0b51dbb47771a2b73398672aac6cf&language=ko`,
    });
    this.credits = credit.data.media;
  },
};
</script>

<style scoped>
.line-clamp {
  display: -webkit-box;
  -webkit-line-clamp: 3;
  -webkit-box-orient: vertical;
  overflow: hidden;
}
</style>
