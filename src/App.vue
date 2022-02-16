<template>
   <div id="app">
      <Header @query-search="getResultsSearch" :genres="movie.movieGenres" />
      <Main :movies="movie.movies" :tv-series="tv.tvSeries" :movie-cast="movie.movieCast" :tv-cast="tv.tvCast" :genres="movie.movieGenres" />
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
         genres: [],
         movie: {
            movies: [],
            moviesId: [],
            movieCast: [],
            movieGenres: [],
         },
         tv: {
            tvSeries: [],
            tvId: [],
            tvCast: [],
            tvGenres: [],
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
               const cast = res.data.cast.filter((actor, index) => {
                  if (index < 5) return true;
               });
               this.movie.movieCast.push(cast);
            });
         });
      },
      getTvCast() {
         return this.tv.tvId.forEach((id) => {
            axios.get(`https://api.themoviedb.org/3/tv/${id}/credits?api_key=e03c5cb8dddd1d7d20fb6adf3922071d&language=it-IT`).then((res) => {
               const cast = res.data.cast.filter((actor, index) => {
                  if (index < 5) return true;
               });
               this.tv.tvCast.push(cast);
            });
         });
      },

      mergeGenres() {
         return this.tv.tvGenres.forEach((tvItem) => {
            const duplicatedGenre = this.movie.movieGenres.filter((movieItem) => {
               if (tvItem.id === movieItem.id) {
                  return true;
               } else return false;
            });

            if (duplicatedGenre.length === 0) {
               this.movie.movieGenres.push(tvItem);
            }
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
         //# EMPTY CAST AND IDs
         this.movie.moviesId = [];
         this.movie.movieCast = [];
         this.tv.tvId = [];
         this.tv.tvCast = [];

         //# GET LIST OF MOVIES AND TV SHOWS
         this.callApi("/search/movie", config, "movie", "movies", "results");
         this.callApi("/search/tv", config, "tv", "tvSeries", "results");
      },
      getGenres() {
         const config = {
            params: {
               language: this.api.language,
               api_key: this.api.apiKey,
            },
         };
         //# GET LIST OF GENRES FOR MOVIES AND TV SHOWS
         this.callApi("/genre/movie/list", config, "movie", "movieGenres", "genres");
         this.callApi("/genre/tv/list", config, "tv", "tvGenres", "genres");
      },

      callApi(endpoint, config, arrayObject, array, dataName) {
         axios.get(`${this.api.baseUri}${endpoint}`, config).then((res) => {
            this[arrayObject][array] = res.data[dataName];
         });
      },
   },
   mounted() {
      this.getGenres();
   },
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
