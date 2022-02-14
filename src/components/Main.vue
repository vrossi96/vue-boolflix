<template>
   <main id="main-content">
      <ul>
         <li>
            {{ movies[0].title }}
            {{ movies[0].original_title }}
            {{ movies[0].original_language }}
            {{ movies[0].vote_average }}
         </li>
      </ul>
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
