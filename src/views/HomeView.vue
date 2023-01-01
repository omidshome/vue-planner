<template>
  <div class="home">
    <FilterNavVue @filterChange="current = $event" :current="current" />
    <div v-if="projects.length">
      <div v-for="project in filteredProjects" :key="project.id">
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
import FilterNavVue from "@/components/FilterNav.vue";

export default {
  computed: {
    filteredProjects() {
      if (this.current === "completed") {
        return this.projects.filter((p) => p.complete);
      }
      if (this.current === "ongoing") {
        return this.projects.filter((p) => !p.complete);
      }

      return this.projects;
    },
  },

  data() {
    return {
      projects: [],
      current: "all",
    };
  },
  methods: {
    handleComplete(id) {
      let p = this.projects.find((project) => project.id === id);
      p.complete = !p.complete;
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
    FilterNavVue,
  },
};
</script>
