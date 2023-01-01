<template>
  <div>
    <form @submit.prevent="handleSubmit">
      <label for="title">Title</label>
      <input type="text" id="title" v-model="title" />
      <label for="detail">Detail</label>
      <textarea id="detail" v-model="details"></textarea>

      <button>Edit Project</button>
    </form>
  </div>
</template>

<script>
export default {
  props: ["id"],
  methods: {
    handleSubmit() {
      fetch(this.uri, {
        method: "PATCH",
        headers: { "Content-Type": "application/json" },
        body: JSON.stringify({ title: this.title, detail: this.details }),
      })
        .then(() => {
          console.log("Done!");
          this.$router.push({ name: "home" });
        })
        .catch((e) => console.log(`Something went wrong. Error: ${e.message}`));
    },
  },

  mounted() {
    fetch(this.uri)
      .then((res) => res.json())
      .then((data) => {
        this.title = data.title;
        this.details = data.detail;
      });
  },

  data() {
    return {
      title: "",
      details: "",
      uri: `http://localhost:3000/projects/${this.id}`,
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
