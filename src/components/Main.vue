<template>
   <main id="main-content">
      <div class="container h-100">
         <div v-if="!movies.length && !tvSeries.length" class="h-100 d-flex align-items-center justify-content-center">
            <h1>CERCA UN FILM</h1>
         </div>
         <div v-else>
            <h2>FILM</h2>
            <ul class="row">
               <li class="col-3" v-for="(movie, index) in movies" :key="movie.id || index">
                  Titolo: {{ movie.title }}, Titolo originale: {{ movie.original_title }}
                  <img
                     v-if="lang.includes(movie.original_language)"
                     class="d-inline-block"
                     :src="require(`../assets/img/${movie.original_language}.png`)"
                     :alt="movie.original_language"
                  />
                  Voto:
                  {{ movie.vote_average }}
               </li>
            </ul>
            <h2>SERIE</h2>
            <ul class="row">
               <li class="col-3" v-for="(tv, index) in tvSeries" :key="tv.id || index">
                  Titolo: {{ tv.name }}, Titolo originale: {{ tv.original_name }}
                  <img
                     v-if="lang.includes(tv.original_language)"
                     class="d-inline-block"
                     :src="require(`../assets/img/${tv.original_language}.png`)"
                     :alt="tv.original_language"
                  />
                  Voto:
                  {{ tv.vote_average }}
               </li>
            </ul>
         </div>
      </div>
   </main>
</template>

<script>
export default {
   name: "Main",
   props: ["movies", "tvSeries"],
   data() {
      return {
         cardBg: "https://image.tmdb.org/t/p/w342",
         lang: ["it", "en", "ja", "de", "es", "pt", "fr", "ko", "cs", "pl", "hi", "ru"],
      };
   },
};
</script>

<style scoped lang="scss">
main {
   height: calc(100vh - 70px);
   background-color: #434343;
   overflow-y: scroll;

   ul {
      list-style: none;

      li {
         position: relative;
         height: 88px;
      }
   }

   img {
      height: 15px;
      width: 25px;
      border-radius: 2px;
   }
}
</style>
