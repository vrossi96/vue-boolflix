<template>
   <main id="main-content">
      <div class="container">
         <h1 v-if="!movies.length && !tvSeries.length">CERCA UN FILM</h1>
         <div v-else>
            <h2>FILM</h2>
            <ul>
               <li v-for="(movie, index) in movies" :key="movie.id || index">
                  Titolo: {{ movie.title }}, Titolo originale: {{ movie.original_title }}
                  <img class="d-inline-block" :src="require(`../assets/img/${movie.original_language}.png`)" :alt="movie.original_language" />
                  Voto:
                  {{ movie.vote_average }}
               </li>
            </ul>
            <h2>SERIE</h2>
            <ul>
               <li v-for="(tv, index) in tvSeries" :key="tv.id || index">
                  Titolo: {{ tv.name }}, Titolo originale: {{ tv.original_name }}
                  <img class="d-inline-block" :src="require(`../assets/img/${tv.original_language}.png`)" :alt="tv.original_language" />
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
};
</script>

<style scoped lang="scss">
main {
   height: calc(100vh - 70px);
   background-color: #434343;
   overflow-y: scroll;

   ul {
      list-style: none;
   }

   img {
      height: 15px;
      width: 25px;
      border-radius: 2px;
   }
}
</style>
