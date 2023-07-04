<template>

  <div class="container">
    <!-- <h1 class="title">Main Page</h1> -->
    <!-- Left Column -->

    <b-button @click="randomizeRecipes" class="more-recipes-button">More Recipes!</b-button>

    <div class="columns-container">

      <div class="left-column">
      <h4 class="column-title">Discover these recipes:</h4>

      <RecipePreviewList ref="randomList"  class="RandomRecipes" title="" />
      <br>
      <br>
      <br>

    </div>


    <!-- Right Column -->
    <div class="right-column">
      <template v-if="$root.store.username">
        <h2 class="column-title">Recently Viewed Recipes</h2>
        <RecipePreviewList
          class="LastViewedRecipes"
          type="lastWatched"
        ></RecipePreviewList>
      </template>
      <template v-else>
        <LoginPage
        style="margin-top:50%;"
        ></LoginPage>
      </template>
    </div>

    </div>

  </div>
</template>

<script>
import RecipePreviewList from "../components/RecipePreviewList";
import LoginPage from "./LoginPage.vue";
export default {
  components: {
    RecipePreviewList,
    LoginPage,
  },
  methods: {
    async randomizeRecipes() {
      await this.$refs.randomList.updateRecipes();
    },
  },
  mounted() {
    this.randomizeRecipes();
  },
};
</script>

<style lang="scss" scoped>
.container {
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  margin: 2% auto;
}

.columns-container{
  display: flex;
  justify-content: space-between;

}

.left-column {
  flex-basis: 50%;
  padding-right: 20px;
}

.right-column {
  flex-basis: 50%;
  // margin-top:15%
}

.column-title {
  font-size: 20px;
  margin-bottom: 10px;
}

.RandomRecipes,
.LastViewedRecipes {
  margin-bottom: 10px;
}

.more-recipes-button {
  margin-top: 2%;
  margin-bottom:2% ;

  width:fit-content;
  left: 0;
}
</style>
