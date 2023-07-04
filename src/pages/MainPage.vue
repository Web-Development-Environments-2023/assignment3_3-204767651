


<template>

  <div class="container">
    <!-- <h1 class="title">Main Page</h1> -->
    <!-- Left Column -->

    <div class="columns-container">

      <div class="left-column">
      <!-- <h4 class="column-title">Discover these recipes:</h4> -->

      <RecipePreviewList ref="randomList"  class="RandomRecipes" title="Discover these recipes:" 
      :recipes="randomRecipes || []"
      :randomized="true"
      @updateRandom="randomizeRecipes"
      />

    </div>


    <!-- Right Column -->
    <div class="right-column">
      <template v-if="$root.store.username">
        <!-- <h2 class="column-title">Recently Viewed Recipes</h2> -->
        <RecipePreviewList
        title="Recently Viewed Recipes:"
          :recipes="lastViewedRecipes || []"

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

  data() {
    return {
      randomRecipes: [],
      lastViewedRecipes: [],
      isLoggedIn: false,
    };
  },
  async mounted(){
    this.isLoggedIn = localStorage.getItem("isLoggedIn") === "true";
    await this.getData();
  },

  watch: {
    isLoggedIn(newVal) {
      if (newVal) {
        this.getData();
      }
    },
  },

  methods: {
    async getRandomRecipes() {
      try{
        
        const response = await this.axios.get(this.$root.store.server_domain + "/recipes/random", {withCredentials: true});
        return response.data;
      } catch (error) {
        this.$root.toast("Input Error", error.message, "danger");
      }
    },

    async getLastViewedRecipes() {
      try{
        const response = await this.axios.get(this.$root.store.server_domain + "/users/lastSeen",  {withCredentials: true});
        return response.data;
      } catch (error) {
        this.$root.toast("Input Error", error.message, "danger");
      }
    },


    async getData() {
      this.randomRecipes = await this.getRandomRecipes();
      if (this.$root.store.username)
        this.lastViewedRecipes = await this.getLastViewedRecipes();
    },

    async randomizeRecipes() {
      this.randomRecipes = await this.getRandomRecipes();
    },

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

