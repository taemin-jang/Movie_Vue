<template>
  <aside class="widget widget-movie-details">
    <h3 class="title">상세</h3>
    <ul>
      <li><strong>개봉일: </strong>{{ detail.release_date }}</li>
      <li>
        <strong>제작비: </strong>{{ String(detail.budget).slice(0, 3) }}
        million USD
      </li>
      <li>
        <strong>제작한 나라: </strong
        >{{ detail.production_companies[0].origin_country }}
      </li>
      <li><strong>언어: </strong>{{ detail.spoken_languages[0].name }}</li>
      <li>
        <strong>제작사: </strong
        ><a href="javascript:void(0)">{{
          detail.production_companies && detail.production_companies[0].name
        }}</a>
      </li>
    </ul>
  </aside>
</template>

<script>
export default {
  data() {
    return {};
  },
  props: ["detail"],
  mounted() {
    console.log(this.detail);
  },
};
</script>

<style lang="scss" scoped></style>
