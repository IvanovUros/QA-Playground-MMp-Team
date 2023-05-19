<template>
  <header class="header-wrapper">
    <AppLogo :change-logo-colors="menuOpen" class="header-wrapper-logo" />

    <AppNavigation
      @nav-close="(showNavElement = false), disableScroll()"
      v-show="showNavElement"
      class="header-wrapper-nav"
    />

    <AppDesktopNavigation
      v-if="currentPath !== '/login'"
      v-show="showDesktopNavElement"
    />

    <div
      @click="logout()"
      v-if="currentPath !== '/login'"
      v-show="showLogin"
      class="header-wrapper-login"
    >
      <img src="../assets/icons/login.svg" alt="logout icon" />
    </div>

    <div
      @click="(showNavElement = false), logout()"
      v-if="currentPath !== '/login'"
      v-show="showLogout"
      class="header-wrapper-logout"
    >
      <img :src="logoutsUrl" alt="logout icon" />
    </div>

    <div class="header-wrapper-burger-menu">
      <img
        @click="(showNavElement = !showNavElement), disableScroll()"
        v-if="currentPath !== '/login'"
        v-show="showBurger"
        :src="burgersUrl"
        alt="burger menu icon"
      />
    </div>
  </header>
</template>

<script lang="ts">
import AppNavigation from "../UI/AppNavigation.vue";
import AppDesktopNavigation from "./AppDesktopNavigation.vue";
import AppLogo from "../UI/AppLogo.vue";
import { defineComponent } from "vue";
export default defineComponent({
  name: "AppHeader",
  components: {
    AppLogo,
    AppNavigation,
    AppDesktopNavigation,
  },

  data() {
    return {
      showNavElement: false,
      showDesktopNavElement: true,
      showBurger: true,
      showLogout: true,
      showLogin: false,
    };
  },

  methods: {
    logout() {
      localStorage.removeItem("isLoggedIn");
      this.$router.replace({ name: "login" });
    },

    disableScroll() {
      if (this.showNavElement == true) {
        document.body.style.overflow = "hidden";
      } else {
        document.body.style.overflow = "";
      }
    },
  },

  computed: {
    menuOpen(): boolean {
      return !this.showNavElement;
    },

    currentPath() {
      return this.$route.path;
    },

    burgersUrl(): string {
      return this.showNavElement
        ? "src/assets/icons/burger-white.svg"
        : "src/assets/icons/burger.svg";
    },

    logoutsUrl(): string {
      return this.showNavElement
        ? "src/assets/icons/logout-white.svg"
        : "src/assets/icons/logout.svg";
    },
  },

  beforeRouteUpdate() {
    this.showNavElement = false;
  },
});
</script>

<style lang="scss" scoped>
.header-wrapper {
  position: relative;
  display: flex;
  flex-direction: row;
  justify-content: space-between;
  align-items: center;
  justify-content: center;
  width: 100%;
  height: 80px;
  padding: 0 5%;
  background-color: $primary-200;
  font-size: 1.75rem;

  &-nav {
    animation: openNavAnimation 1s;
  }

  &-logo {
    position: absolute;
    left: 5%;
    z-index: 2;
  }

  &-burger-menu {
    position: absolute;
    right: 5%;
    z-index: 2;
    cursor: pointer;

    img {
      width: 20px;
    }

    @include sm() {
      display: none;
    }
  }

  &-logout {
    position: absolute;
    right: 5%;
    margin-right: 50px;
    z-index: 2;
    cursor: pointer;

    img {
      width: 20px;
    }
  }

  &-login {
    position: absolute;
    right: 5%;
    margin-right: 50px;
    z-index: 2;
    cursor: pointer;

    img {
      width: 20px;
    }
  }
}

@keyframes openNavAnimation {
  0% {
    height: 0;
  }

  100% {
    height: 100vh;
  }
}
</style>
