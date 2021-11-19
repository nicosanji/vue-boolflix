<template>
  <div id="app">
    <Header @search="getQuery"></Header>
    <Main :query="query"></Main>
  </div>
</template>

<script>
import Main from "./components/Main.vue";
import Header from "./components/Header.vue";

export default {
  components: { Header, Main },
  name: "App",
  data() {
    return {
      query: "",
    };
  },
  methods: {
    getQuery(queryString) {
      this.query = queryString;
    },
  },
};
</script>

<style lang="scss">
@import "~bootstrap/scss/bootstrap";
@import "~font-awesome/css/font-awesome.min.css";
@import "./styles/app.scss";
</style>
