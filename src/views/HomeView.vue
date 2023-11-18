<template>
  <div class="home">
    <h2>Home</h2>
    <FilterNav @filter="current = $event" :current="current"></FilterNav>
    <idv v-for="project in filteredProject" :key="project.id">
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
import FilterNav from "@/components/FilterNav.vue";
export default {
  name: "HomeView",
  components: { SingleProject, FilterNav },
  data() {
    return {
      projects: [],
      current: "all",
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
  computed: {
    filteredProject() {
      if (this.current === "complete") {
        return this.projects.filter((p) => {
          return p.complete;
        });
      }
      if (this.current === "onGoing") {
        return this.projects.filter((p) => {
          return !p.complete;
        });
      }
      return this.projects;
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
