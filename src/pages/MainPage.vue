<template>
  <div class="container">
    <h1 class="title">Main Page</h1>
    <RecipePreviewList ref="randomList" vertical="true" title="Randome Recipes" class="RandomRecipes center" />
    <LoginPage v-if="!$root.store.username"></LoginPage>
    <!-- <router-link v-if="!$root.store.username" to="/login" tag="button">Login!</router-link> -->
   
    <RecipePreviewList v-else
      title="Last Viewed Recipes"
      :class="{
        RandomRecipes: true,
        blur: !$root.store.username,
        center: true
      }"
      disabled
      vertical="true"
      type="lastWatched"
    ></RecipePreviewList>



      <tr>
        <td>
          <b-button @click="randomizeRecipes">More Recipes!</b-button>
        </td>
      </tr>
    <!-- <div
      style="position: absolute;top: 70%;left: 50%;transform: translate(-50%, -50%);"
    >
    </div> -->
  </div>
</template>

<script>
import RecipePreviewList from "../components/RecipePreviewList";
import LoginPage from "./LoginPage.vue";
export default {
  components: {
    RecipePreviewList,
    LoginPage
  },
  methods: {
    async randomizeRecipes() {
      await this.$refs.randomList.updateRecipes();
    } 
  },
  mounted() {
    this.randomizeRecipes();
  }
};
</script>

<style lang="scss" scoped>
.RandomRecipes {
  margin: 10px 0 10px;
}
.blur {
  -webkit-filter: blur(5px); /* Safari 6.0 - 9.0 */
  filter: blur(2px);
}
::v-deep .blur .recipe-preview {
  pointer-events: none;
  cursor: default;
}
</style>


