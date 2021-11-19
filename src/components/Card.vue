<template>
  <div class="my-card col text-center p-0">
    <img
      :src="getImgUrl('w342', film.poster_path)"
      alt="poster"
      class="my-poster"
    />
    <div class="overlay d-flex flex-column align-items-center p-3">
      <h3>{{ film.title }}</h3>
      <h5 v-if="film.title !== film.original_title">
        {{ film.original_title }}
      </h5>
      <img
        :src="getFlagUrl(film.original_language)"
        alt="language"
        class="small-img"
      />
      <span
        ><i
          class="fa fa-star"
          v-for="(star, i) in getRank(film.vote_average)"
          :key="i"
        ></i>
        <i
          class="fa fa-star-o"
          v-for="(star, i) in 5 - getRank(film.vote_average)"
          :key="'A' + i"
        ></i
      ></span>
      <p class="text-center mt-3">
        <span class="fw-bold mb-0">Plot:</span><br />{{ film.overview }}
      </p>
      <p v-if="film.overview === ''">No plot was found for this show.</p>
    </div>
  </div>
</template>

<script>
export default {
  name: "Card",
  props: {
    film: Object,
  },
  data() {
    return {
      imgUrl: "https://image.tmdb.org/t/p/",
      flags: {
        en: "en.png",
        es: "es.png",
        fr: "fr.png",
        it: "it.png",
      },
    };
  },
  methods: {
    getImgUrl(size, path) {
      if (path === null) {
        return require("../assets/img/placeholder_poster.png");
      }
      return this.imgUrl + size + path;
    },
    getFlagUrl(searchByLang) {
      if (!this.flags[searchByLang]) {
        return require("../assets/img/default.png");
      }
      return require("../assets/img/" + this.flags[searchByLang]);
    },
    getRank(initRank) {
      const rank = initRank / 2;
      const fullStar = Math.ceil(rank);
      return fullStar;
    },
  },
};
</script>
