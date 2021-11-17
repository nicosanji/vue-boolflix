<template>
  <div id="app">
    <div class="container py-4">
      <div class="input-group w-50">
        <input
          type="search"
          id="searchForm"
          class="form-control"
          v-model="searchQuery"
          @keyup.enter="apiCall('movie', searchQuery)"
        /><button
          type="button"
          class="btn btn-dark"
          @click="apiCall('movie', searchQuery)"
        >
          Cerca
        </button>
      </div>
    </div>
    <div class="container">
      <ul>
        <li v-for="(item, i) in apiData.movie" :key="i">
          {{
          `titolo: ${item.title}, 
          titolo originale: ${item.original_title},
          lingua: ${item.original_language},
          voto: ${item.vote_average}.`,
          }}
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  name: "App",
  components: {},
  data() {
    return {
      // codice personale
      apiKey: "4e887be83ce5c8ffc309c0a492e50a7f",
      apiUrl: "https://api.themoviedb.org/3",
      apiUrlEnd: {
        movie: "/search/movie",
        tv: "/search/tv",
      },
      apiData: {
        movie: [],
        tv: [],
      },
      searchQuery: "",
    };
  },
  methods: {
    apiCall(urlEnd, query) {
      axios
        .get(this.apiUrl + this.apiUrlEnd[urlEnd], {
          params: {
            api_key: this.apiKey,
            query,
          },
        })
        .then((resp) => {
          this.apiData[urlEnd] = resp.data.results;
        });
    },
  },
  mounted() {},
};
</script>

<style lang="scss">
@import "~bootstrap/scss/bootstrap";
</style>
