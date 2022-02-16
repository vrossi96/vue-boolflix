<template>
   <div id="app">
      <Header @query-search="getResultsSearch" />
      <Main :movies="movie.movies" :tv-series="tv.tvSeries" />
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
         movie: {
            movies: [],
            moviesId: [],
            movieCast: [],
         },
         tv: {
            tvSeries: [],
            tvId: [],
            tvCast: [],
         },
         api: {
            baseUri: "https://api.themoviedb.org/3",
            apiKey: "e03c5cb8dddd1d7d20fb6adf3922071d",
            language: "it-IT",
         },
      };
   },
   computed: {
      getMoviesId() {
         return this.movie.movies.forEach((item) => {
            this.movie.moviesId.push(item.id);
         });
      },
      getTvId() {
         return this.tv.tvSeries.forEach((item) => {
            this.tv.tvId.push(item.id);
         });
      },

      getMovieCast() {
         return this.movie.moviesId.forEach((id) => {
            axios.get(`https://api.themoviedb.org/3/movie/${id}/credits?api_key=e03c5cb8dddd1d7d20fb6adf3922071d&language=it-IT`).then((res) => {
               this.movie.movieCast.push(res.data.cast);
            });
         });
      },
      getTvCast() {
         return this.tv.tvId.forEach((id) => {
            axios.get(`https://api.themoviedb.org/3/tv/${id}/credits?api_key=e03c5cb8dddd1d7d20fb6adf3922071d&language=it-IT`).then((res) => {
               this.tv.tvCast.push(res.data.cast);
            });
         });
      },
   },
   methods: {
      getResultsSearch(term) {
         if (!term) {
            this.movie.movies = [];
            this.tv.tvSeries = [];
            return;
         }
         const config = {
            params: {
               language: this.api.language,
               api_key: this.api.apiKey,
               query: term,
            },
         };
         this.movie.moviesId = [];
         this.movie.movieCast = [];
         this.tv.tvId = [];
         this.tv.tvCast = [];

         this.callApi("/search/movie", config, "movie", "movies");
         this.callApi("/search/tv", config, "tv", "tvSeries");
      },

      callApi(endpoint, config, arrayObject, array) {
         axios.get(`${this.api.baseUri}${endpoint}`, config).then((res) => {
            this[arrayObject][array] = res.data.results;
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
