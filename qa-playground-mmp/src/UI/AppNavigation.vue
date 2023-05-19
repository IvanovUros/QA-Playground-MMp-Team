<template>
  <div>
    <ol>
      <li @click="closeNav" v-for="item in navItems" :key="item.name">
        <router-link :to="item.path">{{ item.name }}</router-link>
      </li>
    </ol>
  </div>
</template>

<script lang="ts">
import { defineComponent } from "vue";
export default defineComponent({
  name: "AppNavigation",

  emits: ["navClose"],

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

  methods: {
    closeNav() {
      this.$emit("navClose", true);
    },
  },
});
</script>

<style lang="scss" scoped>
.header-wrapper-nav {
  position: absolute;
  display: flex;
  flex-direction: column;
  justify-content: flex-start;
  align-items: center;
  top: 0;
  left: 0;
  width: 100%;
  height: 100vh;
  z-index: 1;
  background-color: $primary-800;

  ol {
    padding-left: 0;
    display: flex;
    flex-direction: column;
    align-items: center;
    margin-top: 150px;
    color: $primary-200;

    a {
      line-height: 80px;
      color: $primary-400;
      font-size: 3rem;
      animation: showNavItemsAnimation 1s linear;
    }

    a:hover {
      transition: color 0.2s ease-in;
      color: $primary-200;
    }

    .router-link-active {
      transition: color 0.2s ease-in;
      padding: 15px;
      padding-bottom: 25px;
      border-radius: 30px;
      color: $primary-200;
    }
  }

  @include sm() {
    display: none;
  }

  @keyframes showNavItemsAnimation {
    0% {
      opacity: 0;
      bottom: -60px;
    }

    20% {
      opacity: 0;
      bottom: -50px;
    }

    40% {
      opacity: 0.5;
      bottom: -30px;
    }

    60% {
      opacity: 0.5;
      bottom: -20px;
    }

    80% {
      bottom: -10px;
    }

    100% {
      bottom: 0;
    }
  }
}
</style>
