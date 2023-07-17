
<template>
  <div>
    <div class="container">
      <div class="row">
        <!-- Search Bar -->
        <div class="col-12">
          <div class="search-bar">
            <input
              v-model="searchQuery"
              type="text"
              class="form-control search-input"
              placeholder="Search"
              @focus="focusSearchBar"
            >
          </div>
        </div>
      </div>

      <div id="filters">
        <div class="row mt-3">
          <!-- Filters -->
          <div class="col-12 d-flex align-items-center">
            <!-- Number of Recipes Dropdown -->
            <div class="mr-3">
              <select v-model="numberOfRecipes" class="form-control bg-custom">
                <option v-for="(option, index) in numberOfRecipesOptions" :key="index" :value="option">{{ option }}</option>
              </select>
            </div>

            <!-- Cuisine Dropdown -->
            <div class="mr-3">
              <select v-model="selectedCuisine" class="form-control bg-custom">
                <option v-for="(cuisine, index) in cuisineOptions" :key="index" :value="cuisine">{{ cuisine }}</option>
              </select>
            </div>

            <!-- Diet Dropdown -->
            <div class="mr-3">
              <select v-model="selectedDiet" class="form-control bg-custom">
                <option v-for="(diet, index) in dietOptions" :key="index" :value="diet">{{ diet }}</option>
              </select>
            </div>

            <!-- Intolerances Dropdown -->
            <div>
              <select v-model="selectedIntolerances" class="form-control bg-custom">
                <option v-for="(intolerance, index) in intoleranceOptions" :key="index" :value="intolerance">{{ intolerance }}</option>
              </select>
            </div>
          </div>

          <!-- Search Button -->
          <div class="col-2 d-flex mt-3">
            <button @click="searchRecipes" :disabled="!searchQuery" class="btn btn-success btn-search">Search</button>
          </div>
        </div>
      </div>

      <!-- Display Search Results -->
      <div class="row mt-3">
        <div class="col-12" v-if="searchResults.length === 0">
          <div class="alert alert-info">No results found.</div>
        </div>
      </div>
      <!-- Filter Buttons -->
      <div class="filter-buttons" v-if="searchResults.length > 0">
        <button class="btn btn-success btn-search" @click="sortByPopularity">Sort by Popularity</button>
        <button class="btn btn-success btn-search" @click="sortByCookingTime">Sort by Cooking Time</button>
      </div>

      <div class="resultsPreview">

            <SearchResultPreview 
            :searchResults="filteredSearchResults" 
            />

        </div>
    </div>
  </div>
</template>

<script>
import SearchResultPreview from "../components/SearchResultPreview.vue";
export default {
  name: "SearchPage",
  components: {
    SearchResultPreview
  },
  data() {
    return {
      searchQuery: "",
      numberOfRecipes: 5,
      numberOfRecipesOptions: [5, 10, 15],
      selectedCuisine: "",
      cuisineOptions: [
        "",
        'African',
        'Asian',
        'American',
        'British',
        'Cajun',
        'Caribbean',
        'Chinese',
        'Eastern European',
        'European',
        'French',
        'German',
        'Greek',
        'Indian',
        'Irish',
        'Italian',
        'Japanese',
        'Jewish',
        'Korean',
        'Latin American',
        'Mediterranean',
        'Mexican',
        'Middle Eastern',
        'Nordic',
        'Southern',
        'Spanish',
        'Thai',
        'Vietnamese'
      ],
      selectedDiet: "",
      dietOptions: [
        "",
        'Gluten Free',
        'Ketogenic',
        'Vegetarian',
        'Lacto-Vegetarian',
        'Ovo-Vegetarian',
        'Vegan',
        'Pescetarian',
        'Paleo',
        'Primal',
        'Low FODMAP',
        'Whole30'
      ],
      selectedIntolerances: "",
      intoleranceOptions: [
        "",
        'Dairy',
        'Egg',
        'Gluten',
        'Grain',
        'Peanut',
        'Seafood',
        'Sesame',
        'Shellfish',
        'Soy',
        'Sulfite',
        'Tree Nut',
        'Wheat'
      ],
      searchResults: [],
      filteredSearchResults: []
    };
  },
  methods: {
    async searchRecipes() {
      const params = {
        query: this.searchQuery,
        numberOfRecipes: this.numberOfRecipes,
        cuisine: this.selectedCuisine,
        diet: this.selectedDiet,
        intolerances: this.selectedIntolerances,
      };

      try{const response = await this.axios.get(this.$root.store.server_domain + "/recipes/search", { params });
      this.searchResults = response.data;

      if(this.$root.store.username){
        sessionStorage.setItem("latestSearch", JSON.stringify(params));

      }

    } catch (error) {
      this.$root.toast("Input Error", error.message, "danger");
    }
    },

    async getLastSearch() {
      let search_params = JSON.parse(sessionStorage.getItem('latestSearch')) || null;
      console.log(search_params);
      if (search_params && this.$root.store.username) {
        const params = {
        query: search_params.query,
        numberOfRecipes: search_params.numberOfRecipes,
        cuisine: search_params.cuisine,
        diet: search_params.diet,
        intolerances: search_params.intolerances,
      };
        try{
          console.log(search_params);
          const response = await this.axios.get(this.$root.store.server_domain + "/recipes/search", { params });
          this.searchResults = response.data;
      
    } catch (error) {
      this.$root.toast("Input Error", error.message, "danger");
    }
      }
      
    },

    focusSearchBar() {
      document.querySelector('.search-input').focus();
    },
    sortByPopularity() {
      this.filteredSearchResults  = [...this.searchResults].sort((a, b) => b.popularity - a.popularity);
    },

    sortByCookingTime() {
      this.filteredSearchResults  = [...this.searchResults].sort((a, b) => a.readyInMinutes - b.readyInMinutes);
    },
  },
  computed: {
    showFilterButtons() {
      return this.searchResults.length > 0 && this.filteredResults.length > 0;
    },
  },

  mounted() {
    this.getLastSearch();
  },

  watch: {
    searchResults: {
      immediate: true,
      handler(newValue) {
        this.filteredSearchResults = [...newValue];
      },
    },
  },
};
</script>

<style scoped>
.container {
  margin-top: 2%;
}

.resultsPreview{
  width: 100%;
}

.search-bar {
  position: relative;
  background-color: #d6f3e1;
  border-radius: 5px;
  border: 1px solid rgba(0, 0, 0, 0.2);
}

.search-bar input {
  background-color: transparent;
  border: none;
  outline: none;
  width: 100%;
}

.bg-custom {
  background-color: #d6f3e1;
}



.filter-buttons {
  display: flex;
  justify-content: center;
  margin-bottom: 1rem;
}

.filter-buttons button {
  margin-right: 0.5rem;
}
</style>
