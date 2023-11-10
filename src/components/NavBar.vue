<template>
  <nav class="main-nav">
    <router-link to="/">Projects</router-link>
    <router-link :to="{ name: 'addproject' }">Add Project</router-link>
  </nav>
</template>

<script>
export default {
  name: "NavBar",
};
</script>

<style>
nav {
  text-align: center;
  margin: 40px auto;
}
.main-nav a {
  display: inline-block;
  text-decoration: none;
  margin: 0 10px;
  color: #999;
  font-size: 18px;
}
a.router-link-active {
  border-bottom: 1px solid #00ce89;
}
</style>
