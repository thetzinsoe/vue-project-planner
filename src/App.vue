<template>
  <div>
    <NavBar></NavBar>
    <router-view />
  </div>
</template>

<script>
import NavBar from "../src/components/NavBar.vue";
export default {
  components: { NavBar },
};
</script>
<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  max-width: 600px;
  /* background-color: rgb(239, 237, 237); */
  margin: 0 auto;
}
h2 {
  color: gray;
}
body {
  height: 100vh;
}
</style>
