<template>
  <div class="container">
    <div v-if="recipe">
      <div class="recipe-header mt-3 mb-4">
        <h1>{{ recipe.title }}</h1>







        <div class="image-container">
          <img :src="recipe.image" class="center" />

        
      <div class="info-container">
        <span v-if="recipe.vegetarian" class="icon-container">
          <i class="fas fa-leaf"></i>
          <span class="icon-label">Vegetarian</span>
        </span>
        <span v-if="recipe.vegan" class="icon-container">
          <i class="fas fa-seedling"></i>
          <span class="icon-label">Vegan</span>
        </span>
        <p v-if="recipe.glutenFree">Gluten-Free</p>
        <p>Servings: {{ recipe.servings }}</p>
        <p>Aggregate Likes: {{ recipe.aggregateLikes }}</p>
      </div>
    </div>


      <div class content-container>

        <h2>Ingredients:</h2>
    <ul>
      <li v-for="ingredient in recipe.ingredients" :key="ingredient.id">
        {{ ingredient.name }}
      </li>
    </ul>
    <h2>Instructions:</h2>
    <ol>
      <li v-for="instruction in recipe.instructions" :key="instruction.number">
        {{ instruction.step }}
      </li>
    </ol>

      </div>
        
   




        <!-- </div> -->
      </div>
    </div>
  </div>
</template>



<script>
export default {
  name: 'recipe',
  data() {
    return {
      recipe: null
    };
  },
  async created() {
    try {
      let response;
      // response = this.$route.params.response;

      try {
        response = await this.axios.get(
          // "https://test-for-3-2.herokuapp.com/recipes/info",
          // this.$root.store.server_domain + "/recipes/info",
          // {
          //   params: { id: this.$route.params.recipeId }
          // }
          `${this.$root.store.server_domain}/recipes/fullDetails/${this.$route.params.recipeId}/`
        , {withCredentials: true});

        // console.log("response.status", response.status);
        if (response.status !== 200) this.$router.replace("/NotFound");
      } catch (error) {
        console.log("error.response.status", error.response.status);
        this.$router.replace("/NotFound");
        return;
      }



      


      let {
        vegetarian,
        vegan,
        glutenFree,
        servings,
        instructions,
        ingredients,
        aggregateLikes,
        readyInMinutes,
        image,
        title
      } = response.data;



      // let _instructions = instructions
      //   .map((fstep) => {
      //     fstep.steps[0].step = fstep.name + fstep.steps[0].step;
      //     return fstep.steps;
      //   })
      //   .reduce((a, b) => [...a, ...b], []);

      let _recipe = {
        instructions,
        // _instructions,
        vegetarian,
        vegan,
        glutenFree,
        servings,
        ingredients,
        aggregateLikes,
        readyInMinutes,
        image,
        title
      };

      console.log("_recipe", _recipe);

      this.recipe = _recipe;
    } catch (error) {
      console.log(error);
    }
  }
};
</script>

<style scoped>
/* Add any necessary CSS styles for the About page */
.container {
  display: flex;
  flex-direction: column;
}

.image-container {
  display: flex;
  align-items: flex-start;
}

.image-container img {
  width: 200px; /* Adjust the width as needed */
  margin-right: 20px;
  border-radius: 10px;
}

.info-container {
  display: flex;
  flex-direction: column;
}

.content-container {
  margin-top: 20px;
}

.icon-container {
  display: flex;
  align-items: center;
}

.icon-label {
  margin-left: 5px;
}

/* Include Font Awesome styles */
@import "~@fortawesome/fontawesome-free/css/all.css";
</style>

