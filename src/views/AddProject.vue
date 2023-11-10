<template>
  <div>
    <h2>Add Project</h2>
    <form @submit.prevent="addProject">
      <label class="label" for="title">Title</label>
      <input type="text" id="title" v-model="title" /><br /><br />
      <label class="label" for="detail">Detail</label>
      <input type="text" id="detail" v-model="detail" /><br />
      <button>Add</button>
    </form>
  </div>
</template>
<script>
export default {
  name: "AddProject",
  data() {
    return {
      title: "",
      detail: "",
    };
  },
  methods: {
    addProject() {
      fetch("http://localhost:3000/projects", {
        method: "POST",
        headers: { "Content-Type": "application/json" },
        body: JSON.stringify({
          title: this.title,
          detail: this.detail,
          complete: false,
        }),
      })
        .then(() => {
          this.$router.push("/");
        })
        .catch((err) => console.log(err));
    },
  },
};
</script>
<style>
h2 {
  /* text-align: center; */
}
form {
  /* width: 400px; */
  margin: 10px auto;
  background: white;
  text-align: left;
  padding: 30px;
  border-radius: 10px;
}
body {
  background-color: rgb(228, 226, 226);
}
.label {
  display: block;
  width: 100px;
  text-transform: uppercase;
  font-size: 14px;
  font-weight: 900;
  color: gray;
  margin-bottom: 10px;
}
input {
  width: 100%;
  height: 30px;
  border: 0;
  border-bottom: 1px solid rgb(199, 197, 197);
  margin-bottom: 20px;
  font-size: 20px;
}
button {
  display: block;
  margin: 0 auto;
  width: 100px;
  background-color: #00ce89;
  color: white;
  border-radius: 7px;
  padding: 10px;
  border: none;
}
button:hover {
  background-color: rgb(194, 191, 191);
  color: black;
}
</style>
