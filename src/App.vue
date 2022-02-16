<template>
   <div id="app">
      <Header @query-search="getResultsSearch" />
      <Main :movies="movies" :tv-series="tvSeries" />
   </div>
</template>

<script>
import axios from "axios";

import Header from "./components/Header.vue";
import Main from "./components/Main.vue";

export default {
   name: "App",
   components: {
      Header,
      Main,
   },
   data() {
      return {
         movies: [],
         moviesId: [],
         movieCast: [],
         tvSeries: [],
         tvId: [],
         tvCast: [],
         api: {
            baseUri: "https://api.themoviedb.org/3",
            apiKey: "e03c5cb8dddd1d7d20fb6adf3922071d",
            language: "it-IT",
         },
      };
   },
   computed: {
      getMoviesId() {
         return this.movies.forEach((item) => {
            this.moviesId.push(item.id);
         });
      },
      getTvId() {
         return this.tvSeries.forEach((item) => {
            this.tvId.push(item.id);
         });
      },

      getMovieCast() {
         return this.moviesId.forEach((id) => {
            axios.get(`https://api.themoviedb.org/3/movie/${id}/credits?api_key=e03c5cb8dddd1d7d20fb6adf3922071d&language=it-IT`).then((res) => {
               this.movieCast.push(res.data.cast);
            });
         });
      },
      getTvCast() {
         return this.tvId.forEach((id) => {
            axios.get(`https://api.themoviedb.org/3/tv/${id}/credits?api_key=e03c5cb8dddd1d7d20fb6adf3922071d&language=it-IT`).then((res) => {
               this.tvCast.push(res.data.cast);
            });
         });
      },
   },
   methods: {
      getResultsSearch(term) {
         if (!term) {
            this.movies = [];
            this.tvSeries = [];
            return;
         }
         const config = {
            params: {
               language: this.api.language,
               api_key: this.api.apiKey,
               query: term,
            },
         };
         this.moviesId = [];
         this.movieCast = [];
         this.tvId = [];
         this.tvCast = [];

         this.callApi("/search/movie", config, "movies");
         this.callApi("/search/tv", config, "tvSeries");
      },

      callApi(endpoint, config, array) {
         axios.get(`${this.api.baseUri}${endpoint}`, config).then((res) => {
            this[array] = res.data.results;
         });
      },
      // https://api.themoviedb.org/3/movie/49397/credits?api_key=e03c5cb8dddd1d7d20fb6adf3922071d&language=it-IT
   },
   mounted() {},
};
</script>

<style lang="scss">
@import "./assets/scss/style.scss";
#app {
   font-family: Avenir, Helvetica, Arial, sans-serif;
   -webkit-font-smoothing: antialiased;
   text-align: center;
}
</style>
