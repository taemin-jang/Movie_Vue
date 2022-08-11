<template>
  <div :style="displayed()">
    <div
      class="mfp-bg mfp-fade mfp-ready"
      style="height: 7499px; position: absolute"
    ></div>
    <div
      class="mfp-wrap mfp-close-btn-in mfp-auto-cursor mfp-fade mfp-ready"
      tabindex="-1"
      :style="` position: absolute;`"
    >
      <div class="mfp-container mfp-iframe-holder">
        <div class="mfp-content">
          <div class="mfp-iframe-scaler">
            <button
              title="Close (Esc)"
              type="button"
              class="mfp-close"
              @click="close"
            ></button
            ><iframe
              class="mfp-iframe"
              :src="`//www.youtube.com/embed/${movieId}?autoplay=1`"
              frameborder="0"
              allowfullscreen=""
            ></iframe>
            <iframe
              class="mfp-iframe"
              :src="`//www.youtube.com/embed/${movieId}?autoplay=1`"
              frameborder="0"
              allowfullscreen=""
            ></iframe>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      videos: 0,
    };
  },
  props: {
    display: {
      type: Boolean,
      default() {
        return false;
      },
    },
    movieId: {
      type: String,
      default() {
        return "";
      },
    },
  },
  methods: {
    displayed() {
      if (this.display === true) {
        return "display: block";
      } else {
        return "display: none";
      }
    },
    close(e) {
      e.preventDefault();
      this.$emit("close");
    },
  },
};
</script>

<style lang="scss" scoped>
.mfp-wrap {
  position: fixed !important;
}
</style>
