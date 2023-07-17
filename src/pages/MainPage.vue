


<template>

  <div class="container">
    <!-- <h1 class="title">Main Page</h1> -->
    <!-- Left Column -->

    <div class="columns-container">

      <div class="left-column">
      <!-- <h4 class="column-title">Discover these recipes:</h4> -->

      <RecipePreviewList class="RandomRecipes" title="Discover these recipes:" 
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
        style="padding-top:50%; padding-bottom:50%;"
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
    // this.isLoggedIn = $root.store.username != null;
    this.isLoggedIn = localStorage.getItem("isLoggedIn");
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
        
        const response = await this.axios.get(this.$root.store.server_domain + "/recipes/random");
        return response.data;
      } catch (error) {
        this.$root.toast("Input Error", error.message, "danger");
      }
      return []
      
    },

    async getLastViewedRecipes() {
      try{

        const response = await this.axios.get(this.$root.store.server_domain + "/users/lastSeen");


        return response.data;
      } catch (error) {
        this.$root.toast("Input Error", error.message, "danger");
      }

    },


    async getData() {
      this.randomRecipes = await this.getRandomRecipes();
      if (this.isLoggedIn && this.$root.store.username){
        console.log("getting last viewed recipes");
        this.lastViewedRecipes = await this.getLastViewedRecipes();

      }
    },

    async randomizeRecipes() {
      this.randomRecipes = await this.getRandomRecipes();
    },




  },

};
</script>

<style lang="scss" scoped>
.container {
  margin: 2% auto;
  width: 100%;


}

.columns-container{
  display: flex;
  justify-content: space-between;
  width: 100%;
  margin-left: -10px; /* Adjust the left margin as needed */
  margin-right: -10px; /* Adjust the right margin as needed */



}


.left-column, .right-column {
  flex-basis: 50%;
  padding-left: 10px; /* Adjust the left padding as needed */
  padding-right: 10px; /* Adjust the right padding as needed */

}






</style>

