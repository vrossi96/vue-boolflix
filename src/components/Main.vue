<template>
   <main id="main-content">
      <div class="container">
         <h1 v-if="!movies.length">CERCA UN FILM</h1>
         <ul v-else>
            <li v-for="(movie, index) in movies" :key="movie.id || index">
               Titolo: {{ movie.title }}, Titolo originale: {{ movie.original_title }} Lingua: {{ movie.original_language }}
               <img
                  v-if="movie.original_language === 'it' || movie.original_language === 'en'"
                  class="d-inline-block"
                  :src="require(`../assets/img/${movie.original_language}.png`)"
                  alt=""
               />
               Voto:
               {{ movie.vote_average }}
            </li>
         </ul>
      </div>
   </main>
</template>

<script>
export default {
   name: "Main",
   props: ["movies"],
};
</script>

<style scoped lang="scss">
main {
   height: calc(100vh - 70px);
   background-color: #434343;

   img {
      height: 15px;
      width: 25px;
      border-radius: 2px;
   }
}
</style>
