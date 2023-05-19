<template>
  <div>
    <ol class="header-wrapper-desktop-nav">
      <li v-for="item in navItems" :key="item.name">
        <router-link :to="item.path">{{ item.name }}</router-link>
      </li>
    </ol>
  </div>
</template>

<script lang="ts">
import { defineComponent } from "vue";
export default defineComponent({
  name: "AppDesktopNavigation",

  data() {
    return {
      navItems: [
        { name: "Home", path: "/" },
        { name: "UI Elements", path: "/playground" },
        { name: "Shop Example", path: "/shop" },
        { name: "API-Training", path: "/apiTraining" },
        { name: "Testing Page", path: "/manualTesting" },
        { name: "White Board", path: "/whiteboard" },
      ],
    };
  },
});
</script>

<style lang="scss" scoped>
.header-wrapper-desktop-nav {
  display: none;
  flex-direction: row;
  min-width: fit-content;

  li {
    margin-right: 20px;

    a {
      color: $primary-800;
    }

    a:hover {
      transition: color 0.2s linear;
      color: $secondary-500;
    }

    .router-link-active {
      transition: color 0.2s ease-in;
      color: $secondary-700;
    }
  }

  @include sm() {
    display: flex;
  }
}
</style>
