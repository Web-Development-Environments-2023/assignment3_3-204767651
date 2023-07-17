<template>
    <!-- Display Search Results -->
    <div class="container" v-if="searchResults">
      <div class="gallery">
        <div class="row">
          <div class="col-sm-6 col-md-4 col-lg-3" v-for="recipe in searchResults" :key="recipe.id">
            <RecipePreview :recipe="recipe" class="recipePreview" />
          </div>
        </div>
      </div>
    </div>
  </template>
  

<script>
import RecipePreview from "./RecipePreview.vue";

export default {
  name: "SearchResultPreview",
  components: {
    RecipePreview,
  },
  data() {
    return {
      recipes: [],
    };
  },
  props:{
    searchResults: {type: Array, required: false},
  },


};

</script>

<style scoped>
.container {
  margin-top: 2%;
  margin-bottom: 2rem;
}

.row {
  display: flex;
  flex-wrap: wrap;
  margin-right: -0.5rem;
  margin-left: -0.5rem;
}

.col-sm-6,
.col-md-4,
.col-lg-3 {
  position: relative;
  width: 100%;
  padding-right: 0.5rem;
  padding-left: 0.5rem;
}

.recipePreview {
  display: block;
  border: 0px solid #eaeaea;
  width: 100%;
  margin-bottom: 1rem;
}

</style>




