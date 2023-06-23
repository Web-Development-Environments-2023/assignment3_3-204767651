<template>
  <div class="container">
    <!-- <h1 class="title">Main Page</h1> -->
    <!-- Left Column -->
    <div class="left-column">
      <h4 class="column-title">Discover these recipes</h4>
      <RecipePreviewList ref="randomList"  class="RandomRecipes" />
      <b-button @click="randomizeRecipes" class="more-recipes-button">More Recipes!</b-button>
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
        <LoginPage></LoginPage>
      </template>
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
  justify-content: space-between;
}

.left-column {
  flex-basis: 30%;
  padding-right: 20px;
}

.right-column {
  flex-basis: 70%;
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
  margin-top: 20px;
}
</style>
