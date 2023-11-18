<template>
  <nav class="filter-nav">
    <button @click="filterBy('all')" :class="{ active: current === 'all' }">
      All
    </button>
    <button
      @click="filterBy('complete')"
      :class="{ active: current === 'complete' }"
    >
      Complete
    </button>
    <button
      @click="filterBy('onGoing')"
      :class="{ active: current === 'onGoing' }"
    >
      On Going
    </button>
  </nav>
</template>

<script>
export default {
  name: "FilterNav",
  props: ["current"],
  data() {
    return {};
  },
  methods: {
    filterBy(value) {
      this.$emit("filter", value);
    },
  },
};
</script>

<style>
.filter-nav button {
  background: none;
  border: none;
  color: #bbb;
  font-size: 12px;
  outline: none;
  text-transform: uppercase;
  margin-right: 10px;
  letter-spacing: 1px;
  font-weight: bold;
  cursor: pointer;
}
.filter-nav .active {
  color: #333;
}
</style>
