<template>
  <div>
    <NavbarVue></NavbarVue>

    <router-view></router-view>
  </div>
</template>

<script>
import HomeViewVue from "./views/HomeView.vue";
import NavbarVue from "./components/Navbar.vue";
import FilterNavVue from "./components/FilterNav.vue";

export default {
  components: {
    HomeViewVue,
    NavbarVue,
    FilterNavVue,
  },
};
</script>

<style>
body {
  background: #f2f2f2;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #555;
  max-width: 600px;
  margin: 0 auto;
}
</style>
