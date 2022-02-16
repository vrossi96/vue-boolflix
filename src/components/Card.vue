<template>
   <div class="item-card col-3">
      <!-- IMG BG -->
      <img v-if="item.poster_path" class="poster" :src="cardBg + item.poster_path" alt="" />
      <img v-else class="poster" :src="stockImg" alt="" />

      <!-- INFO CARD with Hover -->
      <div class="info">
         <!-- TITLE -->
         <div class="py-3">
            <span class="fw-bold">Titolo:</span>
            {{ item.title || item.name }}
         </div>
         <!-- ORIGINAL TITLE -->
         <div class="py-3" v-if="checkTitle(item)">
            <span class="fw-bold">Titolo originale:</span>
            {{ item.original_title || item.original_name }}
         </div>
         <!-- LANGUAGE -->
         <div class="py-3">
            <span class="fw-bold">Lingua: </span>
            <img
               v-if="lang.includes(item.original_language)"
               class="d-inline-block flag"
               :src="require(`../assets/img/flags/${item.original_language}.png`)"
               :alt="item.original_language"
            />
            <p v-else>{{ item.original_language }}</p>
         </div>
         <!-- RATING -->
         <div class="py-3">
            <span class="fw-bold">Voto: </span>
            <div class="star-rating">
               <i class="far fa-star"></i>
               <i class="far fa-star"></i>
               <i class="far fa-star"></i>
               <i class="far fa-star"></i>
               <i class="far fa-star"></i>
               <!-- RATING -->
               <!-- <div class="rating">{{ rating }}</div> -->
               <div class="rating">
                  <i v-for="n in rating" :key="n" class="fas fa-star"></i>
               </div>
            </div>
            <span> ({{ rating }}/5) </span>
         </div>
         <!-- CAST -->
         <div class="py-3">
            <span class="fw-bold">Cast: </span>
            <p class="m-0" v-for="actor in cast" :key="actor.name">{{ actor.name }}</p>
         </div>
         <!-- DESCRIPTION -->
         <div v-if="item.overview" class="py-3">
            <p class="fw-bold p-0">Descrizione:</p>
            <span>{{ item.overview }}</span>
         </div>
      </div>
   </div>
</template>

<script>
export default {
   name: "Card",
   props: ["item", "cast"],
   data() {
      return {
         cardBg: "https://image.tmdb.org/t/p/w342",
         lang: ["it", "en", "ja", "de", "es", "pt", "fr", "ko", "cs", "pl", "hi", "ru", "ar", "da", "fi", "vi", "nl"],
         stockImg: "https://i.pinimg.com/originals/c3/c7/d5/c3c7d5d3c5090645d0bc9a44b83c2d40.jpg",
      };
   },
   computed: {
      //* Preso il rating, diviso per 2 e semplificato per eccesso
      rating() {
         return Math.ceil(this.item.vote_average / 2);
      },
   },
   methods: {
      //* Controllo del titolo se ripetuto nel titolo originale
      checkTitle(title) {
         if (title.original_title != title.title || title.original_name != title.name) {
            return true;
         }
      },
   },
};
</script>

<style scoped lang="scss">
.item-card {
   position: relative;
   height: 400px;
   transition: all 0.3s 0s ease-out;
   cursor: pointer;
   &:hover {
      transform: scale(1.05);
      .info {
         display: block;
      }
      .poster {
         display: none;
      }
   }
   .poster {
      border: 1px solid white;
      height: 100%;
      width: 100%;
   }
   .info {
      border: 1px solid white;
      display: none;
      background-color: rgba(0, 0, 0, 0.75);
      height: 100%;
      text-align: start;
      padding: 10px;
      overflow-y: auto;
   }
   .flag {
      height: 20px;
      width: 30px;
      border-radius: 5px;
   }
   //# RATINGS
   .star-rating {
      position: relative;
      display: inline-block;
      .fa-star {
         font-size: 25px;
      }
      .rating {
         position: absolute;
         top: 0;
         left: 0;
         & > * {
            color: rgb(184, 184, 0);
         }
      }
   }
}
</style>
