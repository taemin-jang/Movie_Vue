<template>
  <aside v-if="detail" class="widget widget-movie-details">
    <h3 class="title">상세</h3>
    <ul>
      <li><strong>개봉일: </strong>{{ detail.release_date }}</li>
      <li>
        <strong>제작비: </strong>{{ String(detail.budget).slice(0, 3) }}
        million USD
      </li>
      <li><strong>제작한 나라: </strong>{{ makeCountry }}</li>
      <li><strong>언어: </strong>{{ makeLanguage }}</li>
      <li>
        <strong>제작사: </strong
        ><a href="javascript:void(0)">{{ makeCompanies }}</a>
      </li>
    </ul>
  </aside>
</template>

<script>
export default {
  data() {
    return {};
  },
  computed: {
    makeCountry() {
      return (
        this.detail.production_companies &&
        this.detail.production_companies[0].origin_country
      );
    },

    makeLanguage() {
      return (
        this.detail.production_companies &&
        this.detail.production_companies[0].name
      );
    },

    makeCompanies() {
      return (
        this.detail.spoken_languages && this.detail.spoken_languages[0].name
      );
    },
  },
  props: ["detail"],
  mounted() {},
};
</script>

<style lang="scss" scoped></style>
