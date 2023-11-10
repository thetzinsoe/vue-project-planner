<template>
  <div>
    <h2>Edit Project-{{ id }}</h2>
    <form @submit.prevent="updateProject">
      <label class="label" for="title">Title</label>
      <input type="text" id="title" v-model="title" /><br /><br />
      <label class="label" for="detail">Detail</label>
      <input type="text" id="detail" v-model="detail" /><br />
      <button>Update</button>
    </form>
  </div>
</template>

<script>
export default {
  name: "EditProject",
  props: ["id"],
  data() {
    return {
      title: "",
      detail: "",
      api: "http://localhost:3000/projects/",
    };
  },
  mounted() {
    fetch(this.api + this.id)
      .then((res) => {
        return res.json();
      })
      .then((data) => {
        this.title = data.title;
        this.detail = data.detail;
      })
      .catch((err) => console.log(err));
  },
  methods: {
    updateProject() {
      fetch(this.api + this.id, {
        method: "PUT",
        headers: { "Content-Type": "application/json" },
        body: JSON.stringify({
          title: this.title,
          detail: this.detail,
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

<style></style>
