<template>
   <main id="main-content">
      <div class="container h-100">
         <div v-if="!movieCast.length && !tvCast.length" class="h-100 d-flex align-items-center justify-content-center">
            <h1 class="text-uppercase">CERCA UN FILM o una serie TV!</h1>
         </div>
         <div v-else>
            <div v-if="movies.length">
               <img class="pb-3 pt-5 img-title" src="../assets/img/film-title.png" alt="Film" />
               <div class="category row g-3">
                  <!-- CARDS FOR MOVIES -->
                  <Card v-for="(movie, index) in movies" :key="movie.id || index" :item="movie" :cast="movieCast[index]" :genres="genres" />
               </div>
            </div>
            <div v-if="tvSeries.length">
               <img class="pb-3 pt-5 img-title" src="../assets/img/serie-title.png" alt="Serie TV" />
               <div class="category row g-3">
                  <!-- CARDS FOR TV SERIES -->
                  <Card v-for="(serie, index) in tvSeries" :key="serie.id || index" :item="serie" :cast="tvCast[index]" :genres="genres" />
               </div>
            </div>
         </div>
      </div>
   </main>
</template>

<script>
import Card from "./Card.vue";
export default {
   name: "Main",
   components: {
      Card,
   },
   props: ["movies", "tvSeries", "movieCast", "tvCast", "genres"],
   data() {
      return {};
   },
};
</script>

<style scoped lang="scss">
main {
   height: calc(100vh - 70px);
   background-color: #434343;
   overflow-y: scroll;

   .img-title {
      height: 180px;
   }

   .col-3 {
      overflow-x: hidden;
   }
   .category {
      list-style: none;
      padding-bottom: 50px;
   }
}
</style>
