<template>
  <div>
    <HomeViewVue></HomeViewVue>
  </div>
</template>

<script>
import HomeViewVue from "./views/HomeView.vue";

export default {
  components: {
    HomeViewVue,
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
