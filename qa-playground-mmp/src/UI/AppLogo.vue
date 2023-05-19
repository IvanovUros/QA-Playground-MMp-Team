<template>
  <div class="logo">
    <img :src="logosUrl" alt="header logo" />
  </div>
</template>

<script lang="ts">
import { defineComponent } from "vue";

export default defineComponent({
  name: "AppLogo",

  props: {
    changeLogoColors: {
      type: Boolean,
    },
  },

  computed: {
    logosUrl(): string {
      return this.changeLogoColors
        ? "src/assets/logos/header-logo.png"
        : "src/assets/logos/header-logo-white.png";
    },
  },
});
</script>

<style lang="scss" scoped>
.logo {
  width: 100px;

  img {
    width: 100%;
  }
}
</style>
