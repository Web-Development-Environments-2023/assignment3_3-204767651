<template>
    <div class="container">
      <h1 class="title">Your Favorite Recipes</h1>

      <div class="resultsPreview">

      <SearchResultPreview 
      :searchResults="favorite_list" 
      />

</div>
      

    </div>
  </template>
  
  <script>
  import SearchResultPreview from "../components/SearchResultPreview.vue";
  export default {
    name: 'favorites',
    components: {
    SearchResultPreview
  },
  data(){
    return{
      favorite_list:[],
    }
  },
  mounted(){
    this.getFavorites();
  },

  methods:{
    async getFavorites(){
      try{
        const response = await this.axios.get(this.$root.store.server_domain + "/users/favorites");
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

