<template>
  <div></div>
</template>

<script>
// @ is an alias to /src

export default {
  name: "HomeView",
  data() {
    return {
      projects: [],
    };
  },
  components: {},
  mounted() {
    fetch("http://localhost:3000/projects")
      .then((data) => data.json())
      .then((res) => {
        this.projects = res;
      })
      .catch((err) =>
        console.log(`Error occured while fetching ${err.message}`)
      );
  },
};
</script>
