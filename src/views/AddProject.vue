<template>
  <div>
    <form @submit.prevent="handleSubmit">
      <label for="title">Title</label>
      <input type="text" id="title" v-model="title" required />
      <label for="detail">Detail</label>
      <textarea id="detail" v-model="details" required></textarea>

      <button type="submit">Add Project</button>
    </form>
  </div>
</template>

<script>
import { RouterLink } from "vue-router";
import router from "../router";
export default {
  name: "AddProject",
  methods: {
    handleSubmit() {
      let project = {
        title: this.title,
        detail: this.details,
        complete: false,
      };

      fetch("http://localhost:3000/projects", {
        method: "POST",
        headers: {
          "Content-Type": "application/json",
        },
        body: JSON.stringify(project),
      }).then(() => {
        router.push("/").catch("Something went wrong!");
      });
    },
  },
  data() {
    return {
      title: "",
      details: "",
    };
  },
};
</script>

<style scoped>
form {
  background: white;
  padding: 20px;
  border-radius: 10px;
}

label {
  display: block;
  color: #bbb;
  text-transform: uppercase;
  font-size: 14px;
  font-weight: bold;
  letter-spacing: 1px;
  margin: 20px 0 10px 0;
}

input {
  padding: 10px;
  width: 100%;
  box-sizing: border-box;
  border: none;
  border-bottom: 1px solid #ddd;
}

textarea {
  border: 1px solid #ddd;
  padding: 10px;
  display: block;
  width: 100%;
  box-sizing: border-box;
  height: 100px;
}

form button {
  display: block;
  margin: 20px auto 0;
  background: #00ce89;
  color: white;
  padding: 10px;
  border: 0;
  border-radius: 5px;
  font-size: 16px;
}
</style>
