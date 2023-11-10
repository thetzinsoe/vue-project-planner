<template>
  <div class="home">
    HOME<br />
    <idv v-for="project in projects" :key="project.id">
      <div v-show="project.id == ''">There is no project here!</div>
      <SingleProject
        :project="project"
        @delete="deleteProject"
        @complete="completeProject"
      ></SingleProject>
    </idv>
  </div>
</template>

<script>
import SingleProject from "../components/SingleProject.vue";
export default {
  name: "HomeView",
  components: { SingleProject },
  data() {
    return {
      projects: [],
    };
  },
  methods: {
    deleteProject(id) {
      this.projects = this.projects.filter((project) => {
        return project.id != id;
      });
    },
    completeProject(id) {
      let completeDynamic = this.projects.find((project) => {
        return project.id === id;
      });
      completeDynamic.complete = !completeDynamic.complete;
    },
  },
  mounted() {
    fetch(" http://localhost:3000/projects")
      .then((respond) => {
        return respond.json();
      })
      .then((data) => {
        this.projects = data;
      })
      .catch();
  },
};
</script>
