<template>
  <div>
    <nav class="main-nav">
      <router-link :to="{ name: 'home' }">Home</router-link>
      <router-link :to="{ name: 'addProject' }">Add New Project</router-link>
    </nav>
  </div>
</template>

<script>
export default {};
</script>

<style scoped>
.main-nav {
  margin: 40px auto;
  text-align: center;
}

.main-nav a {
  display: inline-block;
  text-decoration: none;
  margin: 0 10px;
  color: #999;
  font-size: 18px;
  font-weight: bold;
  border-radius: 10px;
  padding: 10px;
}

a.router-link-active {
  border-bottom: 2px solid #00ce89;
  padding-bottom: 4px;
  background: #eee;
}
</style>
