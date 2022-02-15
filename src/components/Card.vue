<template>
   <div class="item-card col-3">
      <img v-if="item.poster_path" class="poster" :src="cardBg + item.poster_path" alt="" />
      <img v-else class="poster" :src="stockImg" alt="" />
      <div class="info">
         <p>Titolo: {{ item.title || item.name }}</p>
         <p>Titolo originale: {{ item.original_title || item.original_name }}</p>
         <p>
            Paese d'origine:
            <img
               v-if="lang.includes(item.original_language)"
               class="d-inline-block flag"
               :src="require(`../assets/img/${item.original_language}.png`)"
               :alt="item.original_language"
            />
         </p>
         <p>Voto: {{ item.vote_average }}</p>
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
      height: 15px;
      width: 25px;
      border-radius: 2px;
   }
}
</style>
