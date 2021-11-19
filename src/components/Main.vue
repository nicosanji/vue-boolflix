<template>
  <main>
    <div class="container py-5">
      <h1 class="text-black fw-bold">Film</h1>
      <div class="row row-cols-3">
        <Card v-for="movie in movies" :film="movie" :key="movie.id"></Card>
      </div>
      <h1 class="text-black fw-bold pt-5">Series</h1>
      <div class="row row-cols-3">
        <Card v-for="serie in series" :film="serie" :key="serie.id"></Card>
      </div>
    </div>
  </main>
</template>

<script>
import axios from "axios";
import Card from "./Card.vue";
export default {
  components: { Card },
  name: "Main",
  data() {
    return {
      apiKey: "4e887be83ce5c8ffc309c0a492e50a7f",
      apiUrl: "https://api.themoviedb.org/3",
      imgUrl: "https://image.tmdb.org/t/p/",
      movies: [],
      series: [],
      flags: {
        en: "en.png",
        it: "it.png",
        fr: "fr.png",
        es: "es.png",
      },
      totalStars: [],
    };
  },
  props: {
    query: String,
  },
  methods: {
    apiCall(get, query, type) {
      axios
        .get(this.apiUrl + "/search/" + get, {
          params: {
            query: query,
            api_key: this.apiKey,
          },
        })
        .then((resp) => {
          this[type] = resp.data.results;
        });
    },
    apiCallMovieTv(getM, getT, query, typeM, typeT) {
      this.apiCall(getM, query, typeM);
      this.apiCall(getT, query, typeT);
    },
  },
  watch: {
    query: function (query) {
      this.apiCallMovieTv("movie", "tv", query, "movies", "series");
    },
  },
};
</script>
