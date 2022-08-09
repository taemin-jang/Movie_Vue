<template>
  <div class="col-md-12 col-sm-12">
    <div class="celebrity-list-1">
      <div class="celeb-container">
        <!-- Celebrity Image -->
        <div class="celebrity-image">
          <router-link :to="`/credit/detail/${item.credit_id}`">
            <img
              :src="`https://image.tmdb.org/t/p/w300/${item.profile_path}`"
              alt=""
            />
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
            <p>
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
  methods: {},
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

<style lang="scss" scoped></style>
