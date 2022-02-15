<template>
   <header id="header">
      <div class="container">
         <div class="row">
            <div class="col-12 d-flex justify-content-between align-items-center">
               <a href="#">
                  <img src="../assets/img/boolflix.png" alt="Boolflix" />
               </a>
               <div>
                  <input type="text" v-model="searched" @keyup.enter="getSearch" placeholder="Cerca un film o serie..." />
                  <button @click="getSearch">Cerca</button>
               </div>
            </div>
         </div>
      </div>
   </header>
</template>

<script>
export default {
   name: "Header",
   data() {
      return {
         searched: "",
      };
   },
   props: [],
   methods: {
      getSearch() {
         this.$emit("query-search-movie", this.searched);
         this.$emit("query-search-tv", this.searched);
         this.searched = "";
      },
   },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
header {
   background-color: #000;
   img {
      height: 70px;
   }
}
</style>
