<template>
  <b-container>
    <h3>
      {{ title }}
    </h3>
    <div class="recipe-column">
      <RecipePreview v-for="r in recipes" :key="r.id" class="recipePreview" :recipe="r" />
      <div>
        <b-button v-if="randomized === true" width="auto" class="more-recipes-button" @click="$emit('updateRandom')">More Recipes!</b-button>

      </div>

    </div>
  </b-container>
</template>

<script>
import RecipePreview from "./RecipePreview.vue";
export default {
  name: "RecipePreviewList",
  components: {
    RecipePreview
  },
  props: {
    title: {type: String, required: false},
    recipes: {type: Array, required: true},
    randomized: {type: Boolean, default: false}
  },
  created() {
    if(!this.recipes || !this.recipes.length ===0) {
      this.$emit("created")
    }
  },

};
</script>

<style scoped>
.recipe-column {
  display: flex;
  flex-direction: column;
  height: 100%;

}

.recipePreview {
  margin-bottom: 10px;
  
};

.more-recipes-button {
  margin-top: 2%;
  margin-bottom:2%;
}
</style>

