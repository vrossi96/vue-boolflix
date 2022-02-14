<template>
   <main id="main-content">
      <div class="container">
         <h1 v-if="!movies.length">CERCA UN FILM</h1>
         <ul v-else>
            <li v-for="(movie, index) in movies" :key="movie.id || index">
               Titolo: {{ movie.title }}, Titolo originale: {{ movie.original_title }} Lingua: {{ movie.original_language }} Voto:
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
}
</style>
