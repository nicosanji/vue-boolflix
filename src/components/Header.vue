<template>
  <header class="bg-black d-flex justify-content-between p-3">
    <img src="../assets/img/nickflix.png" alt="nickflix" />
    <SearchInput @search="getInputQuery"></SearchInput>
  </header>
</template>

<script>
import SearchInput from "./SearchInput.vue";
export default {
  components: { SearchInput },
  name: "Header",
  data() {
    return {
      query: "",
    };
  },
  methods: {
    getInputQuery(queryString) {
      this.query = queryString;
      this.$emit("search", this.query);
    },
  },
};
</script>
