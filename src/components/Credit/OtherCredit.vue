<template>
  <div class="col-md-12 col-sm-12">
    <div class="celebrity-list-1">
      <div class="celeb-container">
        <!-- Celebrity Image -->
        <div class="celebrity-image">
          <router-link :to="`/credit/detail/${item.id}`">
            <img :src="``" alt="" />
          </router-link>
        </div>

        <!-- Celebrity Content -->
        <div class="celebrity-content">
          <div class="inner">
            <h3 class="title">
              <a href="celebrity-detail.html">{{ "" }}</a>
            </h3>

            <p>
              Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do
              eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut
              enim ad minim veniam, quis nostrud exercitation ullamco laboris
              nisi ut aliquip ex ea commodo consequat.
            </p>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: ["item"],
  mounted() {
    console.log(this.item);
  },
};
</script>

<style lang="scss" scoped></style>
