<template>
  <div class="project" :class="{ complete: project.complete }">
    <div class="flexing">
      <div>
        <h2 @click="showDetail = !showDetail">{{ project.title }}</h2>
      </div>
      <div>
        <span class="del" title="are you sure delete" @click="deleteProject"
          >delete</span
        >
        <span class="edi">edit</span>
        <span class="com" @click="completeProject">complete</span>
      </div>
    </div>
    <p v-if="showDetail">{{ project.detail }}</p>
  </div>
</template>

<script>
export default {
  name: "SingleProject",
  props: ["project"],
  data() {
    return {
      showDetail: false,
      api: " http://localhost:3000/projects/",
    };
  },
  methods: {
    deleteProject() {
      console.log(this.project.id);
      fetch(this.api + this.project.id, { method: "DELETE" })
        .then(() => {
          this.$emit("delete", this.project.id);
        })
        .catch((err) => console.log(err.message()));
    },
    completeProject() {
      fetch(this.api + this.project.id, { method: "PATCH" })
        .then(() => {
          this.$emit("complete", this.project.id);
        })
        .catch((err) => {
          console.log(err.message());
        });
    },
  },
  mounted() {},
};
</script>

<style>
.project {
  background-color: #f3f0f0;
  padding: 20px;
  margin: 10px;
  border-left: 7px solid red;
  border-radius: 10px;
}
.flexing {
  display: flex;
  justify-content: space-between;
  align-items: center;
}
h2 {
  cursor: pointer;
  color: indigo;
}
span {
  margin-right: 10px;
  padding: 5px;
  border-radius: 6px;
  color: white;
  cursor: pointer;
}
span:hover {
  color: black;
  background-color: rgb(194, 191, 191);
}
.del {
  background-color: red;
}
.edi {
  background-color: blue;
}
.com {
  background-color: green;
}
.complete {
  border-left-color: green;
}
</style>
