<template>
  <div class="container">
    <div v-if="recipe">
      console.log(recipe)
      <div class="recipe-header mt-3 mb-4">
        <h1>{{ recipe.title }}</h1>
        <img :src="recipe.image" class="center" />
      </div>
    </div>
    console.log(Not recipe)
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
        );

        // console.log("response.status", response.status);
        if (response.status !== 200) this.$router.replace("/NotFound");
      } catch (error) {
        console.log("error.response.status", error.response.status);
        this.$router.replace("/NotFound");
        return;
      }

      // let {
      //   analyzedInstructions,
      //   instructions,
      //   extendedIngredients,
      //   aggregateLikes,
      //   readyInMinutes,
      //   image,
      //   title
      // } = response.data.recipe;


      let {
        instructions,
        ingredients,
        aggregateLikes,
        readyInMinutes,
        image,
        title
      } = response.data.recipe;



      let _instructions = instructions
        .map((fstep) => {
          fstep.steps[0].step = fstep.name + fstep.steps[0].step;
          return fstep.steps;
        })
        .reduce((a, b) => [...a, ...b], []);

      let _recipe = {
        instructions,
        _instructions,
        ingredients,
        aggregateLikes,
        readyInMinutes,
        image,
        title
      };

      this.recipe = _recipe;
    } catch (error) {
      console.log(error);
    }
  }
};
</script>

<style>
/* Add any necessary CSS styles for the About page */
</style>

