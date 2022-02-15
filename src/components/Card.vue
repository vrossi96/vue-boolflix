<template>
   <div class="item-card col-3">
      <!-- IMG BG -->
      <img v-if="item.poster_path" class="poster" :src="cardBg + item.poster_path" alt="" />
      <img v-else class="poster" :src="stockImg" alt="" />

      <!-- INFO CARD with Hover -->
      <div class="info">
         <p>Titolo: {{ item.title || item.name }}</p>
         <p>Titolo originale: {{ item.original_title || item.original_name }}</p>
         <img
            v-if="lang.includes(item.original_language)"
            class="d-inline-block flag"
            :src="require(`../assets/img/${item.original_language}.png`)"
            :alt="item.original_language"
         />
         <p v-else>{{ item.original_language }}</p>
         <div>
            <p>Voto: {{ item.vote_average }} <i class="far fa-star"></i> <i class="fas fa-star"></i></p>
            <div class="star-rating">
               <i class="far fa-star"></i>
               <i class="far fa-star"></i>
               <i class="far fa-star"></i>
               <i class="far fa-star"></i>
               <i class="far fa-star"></i>
               <!-- RATING -->
               <!-- <div class="rating">{{ rating }}</div> -->
               <div class="rating">
                  <i v-for="n in rating(item.vote_average)" :key="n" class="fas fa-star"></i>
               </div>
            </div>
         </div>
      </div>
   </div>
</template>

<script>
export default {
   name: "Card",
   props: ["item"],
   data() {
      return {
         cardBg: "https://image.tmdb.org/t/p/w342",
         lang: ["it", "en", "ja", "de", "es", "pt", "fr", "ko", "cs", "pl", "hi", "ru"],
         stockImg: "https://i.pinimg.com/originals/c3/c7/d5/c3c7d5d3c5090645d0bc9a44b83c2d40.jpg",
      };
   },
   methods: {
      rating(n) {
         const rating = Math.ceil(n) / 2;
         return rating;
      },
   },
};
</script>

<style scoped lang="scss">
.item-card {
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
   .poster {
      height: 100%;
      width: 100%;
   }
   .info {
      display: none;
      background-color: rgba(0, 0, 0, 0.75);
      height: 100%;
   }
   .flag {
      height: 20px;
      width: 30px;
      border-radius: 5px;
      margin-bottom: 16px;
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
      }
   }
}
</style>
