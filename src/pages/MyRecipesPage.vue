<template>
  <div class="container">
    <h1 class="title">My Recipes</h1>

    <div class="resultsPreview">

    <SearchResultPreview 
    :searchResults="recipe_list" 
    />

</div>
    

  </div>
</template>

<script>
import SearchResultPreview from "../components/SearchResultPreview.vue";
export default {
  name: 'myrecipes',
  components: {
  SearchResultPreview
},
data(){
  return{
    recipe_list:[],
  }
},
mounted(){
  this.getFavorites();
},

methods:{
  async getFavorites(){
    try{
      const response = await this.axios.get(this.$root.store.server_domain + "/users/myrecipes");
      this.favorite_list = response.data;
    }
    catch(error){
      this.$root.toast("Input Error", error.message, "danger");
    }
  },
},
};
</script>

<style>
.container {
  margin-top: 2%;
  margin-bottom: 2rem;
  justify-content: center;
  align-items: center;
}

.title {
  font-weight: bold;
  font-size: 2rem;
  margin-bottom: 2rem;
}
</style>


