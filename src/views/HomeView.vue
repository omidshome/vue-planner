<template>
  <div>
    <div v-if="projects.length">
      <div v-for="project in projects" :key="project.id">
        <h3>{{ project.title }}</h3>
      </div>
    </div>
  </div>
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
