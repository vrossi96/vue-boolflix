<template>
   <div id="app">
      <Header @query-search="getSearchedMovies" />
      <Main :movies="movies" />
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
         querySearch: "",
         movies: [],
      };
   },
   computed: {},
   methods: {
      getSearchedMovies(term) {
         axios.get(`https://api.themoviedb.org/3/search/movie?api_key=e03c5cb8dddd1d7d20fb6adf3922071d&query=${term}&language=it-IT`).then((res) => {
            this.movies = res.data.results;
         });
      },

      addQuerySearch(term) {
         this.querySearch = term;
      },
   },
   mounted() {
      // this.getSearchedMovies();
   },
};
</script>

<style lang="scss">
@import "./assets/scss/style.scss";
#app {
   font-family: Avenir, Helvetica, Arial, sans-serif;
   -webkit-font-smoothing: antialiased;
   -moz-osx-font-smoothing: grayscale;
   text-align: center;
}
</style>
