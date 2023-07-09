<!-- <template>
  <div class="container">
    <h1 class="title">Search Page</h1>
  </div>
</template> -->



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

        <div class="col-12" v-else>
          <ul class="list-group">
            <li v-for="result in searchResults" :key="result.id" class="list-group-item" @click="goToRecipe(result.id)">
              <img :src="result.image" alt="Recipe Image" class="img-thumbnail">
              <div>
                <h4 class="mb-1">{{ result.title }}</h4>
                <p class="mb-0">{{ result.description }}</p>
              </div>
            </li>
          </ul>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
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
    };
  },
  methods: {
    searchRecipes() {
      // Perform API request to get search results based on the selected parameters
      // Update this.searchResults with the retrieved results
      const params = {
        query: this.searchQuery,
        numberOfRecipes: this.numberOfRecipes,
        cuisine: this.selectedCuisine,
        diet: this.selectedDiet,
        intolerances: this.selectedIntolerances,
      };
      console.log(params);
    },
    goToRecipe(recipeId) {
      // Navigate to the recipe page using the router (e.g., this.$router.push(`/recipe/${recipeId}`))
    },
    focusSearchBar() {
      document.querySelector('.search-input').focus();
    },
  },
};
</script>

<style scoped>
.container {
  margin-top: 2%;
}

.search-bar{
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
</style>




