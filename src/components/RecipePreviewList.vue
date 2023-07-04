<!-- <template>
  <b-container>
    <h3>
      {{ title }}
    </h3>
    <div class="recipe-column">
      <RecipePreview v-for="r in recipes" :key="r.id" class="recipePreview" :recipe="r" />
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
    title: {type: String, required: false}
  },
  data() {
    return {
      recipes: []
    };
  },
  mounted() {
    this.updateRecipes();
  },
  methods: {
    async updateRecipes() {
      try {
        const response = await this.axios.get(
          this.$root.store.server_domain + "/recipes/random",
          // "https://test-for-3-2.herokuapp.com/recipes/random"
        );

        const recipes = response.data;
        this.recipes = [];
        this.recipes.push(...recipes);
        
        // console.log(this.recipes);
      } catch (error) {
        console.log(error);
      }
    }
  }
};
</script>

<style scoped>
.recipe-column {
  display: flex;
  flex-direction: column;

}

.recipePreview {
  margin-bottom: 10px;
  
}
</style> -->



<template>
  <b-container>
    <h3>
      {{ title }}
    </h3>
    <div class="recipe-column">
      <RecipePreview v-for="r in recipes" :key="r.id" class="recipePreview" :recipe="r" />
      <b-button v-if="randomized === true" width="fit-content" class="more-recipes-button" @click="$emit('updateRandom')">More Recipes!</b-button>

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

}

.recipePreview {
  margin-bottom: 10px;
  
};

.more-recipes-button {
  margin-top: 2%;
  margin-bottom:2% ;

  left: 0;
}
</style>

