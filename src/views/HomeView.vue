<template>
  <div>
    <div v-if="projects.length">
      <div v-for="project in projects" :key="project.id">
        <SingleProjectVue
          :project="project"
          @deletedId="onDeleltedProject"
          @complete="handleComplete"
        />
      </div>
    </div>
  </div>
</template>

<script>
import SingleProjectVue from "@/components/SingleProject.vue";

export default {
  name: "HomeView",
  data() {
    return {
      projects: [],
    };
  },
  components: {},
  methods: {
    handleComplete(id) {
      let p = this.projects.find((project) => project.id === id);
      p.complete = !p.complete;
      console.log(p);
    },
    onDeleltedProject(id) {
      this.projects = this.projects.filter((project) => project.id !== id);
    },
  },
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

  components: {
    SingleProjectVue,
  },
};
</script>
