<template>
   <header id="header">
      <div class="container">
         <div class="row">
            <div class="col-12 d-flex justify-content-between align-items-center">
               <a href="#">
                  <img src="../assets/img/boolflix.png" alt="Boolflix" />
               </a>
               <div class="input-box">
                  <select name="" id="">
                     <option value="">Generi</option>
                     <option v-for="g in genres" :key="g.id" :value="g.id">{{ g.name }}</option>
                  </select>
                  <input type="text" v-model.trim="searched" @keyup.enter="getSearch" placeholder="Cerca un film o serie..." />
                  <button @click="getSearch"><i class="fas fa-search"></i></button>
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
   props: ["genres"],
   methods: {
      getSearch() {
         this.$emit("query-search", this.searched);
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

   .input-box {
      > * {
         height: 30px;
         border: 2px solid #dc1a28;
      }
      > :first-child {
         border-radius: 5px 0 0 5px;
      }
      > :last-child {
         border-radius: 0 5px 5px 0;
         background-color: #dc1a28;
      }
   }
}
</style>
