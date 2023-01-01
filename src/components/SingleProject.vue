<template>
  <div class="project" :class="{ complete: project.complete == true }">
    <div class="action">
      <h3 @click="showDetail = !showDetail">{{ project.title }}</h3>
      <div class="icons">
        <router-link :to="{ name: `editProject`, params: { id: project.id } }">
          <span class="material-symbols-outlined"> edit </span>
        </router-link>
        <span class="material-symbols-outlined" @click="deleteProject">
          delete
        </span>
        <span class="material-symbols-outlined tick" @click="toggleComplete">
          done
        </span>
      </div>
    </div>

    <div class="detail" v-if="showDetail">
      {{ project.detail }}
    </div>
  </div>
</template>

<script>
export default {
  props: ["project"],
  methods: {
    toggleComplete() {
      fetch(this.url, {
        method: "PATCH",
        headers: { "Content-Type": "application/json" },
        body: JSON.stringify({ complete: !this.project.complete }),
      }).then(() => this.$emit("complete", this.project.id));
    },
    deleteProject() {
      fetch(this.url, { method: "DELETE" })
        .catch("Somethig went wrong")
        .then(() => this.$emit("deletedId", this.project.id));
      console.log(`project ${this.project.id} was deleted`);
    },
  },
  data() {
    return {
      showDetail: false,
      url: "http://localhost:3000/projects/" + this.project.id,
    };
  },
};
</script>

<style>
.project {
  margin: 20px auto;
  background: white;
  padding: 10px 20px;
  border-radius: 4px;
  box-shadow: 1px 2px 3px rgba(0, 0, 0, 0.5);
  border-left: 4px solid #e90074;
}

h3 {
  cursor: pointer;
}

.action {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.material-symbols-outlined {
  font-size: 24px;
  margin-left: 10px;
  color: #bbb;
  cursor: pointer;
}

.material-symbols-outlined:hover {
  color: #777;
}

.project.complete {
  border-left: 4px solid #00ce89;
}

.project.project.complete .tick {
  color: #00ce89;
}
</style>
