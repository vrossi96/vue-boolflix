<template>
   <main id="main-content">
      <div class="container h-100">
         <div v-if="!movies.length && !tvSeries.length" class="h-100 d-flex align-items-center justify-content-center">
            <h1>CERCA UN FILM</h1>
         </div>
         <div v-else>
            <h2 class="py-3">FILM</h2>
            <ul class="row g-3">
               <li class="col-3" v-for="(movie, index) in movies" :key="movie.id || index">
                  <img v-if="movie.poster_path" class="poster" :src="cardBg + movie.poster_path" alt="" />
                  <img v-else class="poster" src="https://i.pinimg.com/originals/c3/c7/d5/c3c7d5d3c5090645d0bc9a44b83c2d40.jpg" alt="" />
                  <div class="info">
                     <p>Titolo: {{ movie.title }}</p>
                     <p>Titolo originale: {{ movie.original_title }}</p>
                     <p>
                        Paese d'origine:
                        <img
                           v-if="lang.includes(movie.original_language)"
                           class="d-inline-block"
                           :src="require(`../assets/img/${movie.original_language}.png`)"
                           :alt="movie.original_language"
                        />
                     </p>
                     <p>Voto: {{ movie.vote_average }}</p>
                  </div>
               </li>
            </ul>
            <h2 class="py-3">SERIE</h2>
            <ul class="row g-3">
               <li class="col-3" v-for="(tv, index) in tvSeries" :key="tv.id || index">
                  <img v-if="tv.poster_path" class="poster" :src="cardBg + tv.poster_path" alt="" />
                  <img v-else class="poster" src="https://i.pinimg.com/originals/c3/c7/d5/c3c7d5d3c5090645d0bc9a44b83c2d40.jpg" alt="" />
                  <div class="info">
                     <p>Titolo: {{ tv.name }}</p>
                     <p>Titolo originale: {{ tv.original_name }}</p>
                     <p>
                        Paese d'origine:
                        <img
                           v-if="lang.includes(tv.original_language)"
                           class="d-inline-block"
                           :src="require(`../assets/img/${tv.original_language}.png`)"
                           :alt="tv.original_language"
                        />
                     </p>
                     <p>Voto: {{ tv.vote_average }}</p>
                  </div>
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

   .col-3 {
      overflow-x: hidden;
   }
   ul {
      list-style: none;

      li {
         position: relative;
         height: 400px;
         &:hover {
            .info {
               display: block;
            }
            .poster {
               display: none;
            }
         }
      }
      .poster {
         height: 100%;
         width: 100%;
      }
      .info {
         display: none;
         background-color: rgba(0, 0, 0, 0.75);
         height: 100%;
      }
   }

   img {
      height: 15px;
      width: 25px;
      border-radius: 2px;
   }
}
</style>
