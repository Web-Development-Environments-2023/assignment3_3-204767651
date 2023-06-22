<template>
    <div class="container">
      <h1 class="title">Add New Recipe</h1>
      <form @submit.prevent="submitForm" class="form">
        <div class="form-group">
          <label for="title">Title:</label>
          <input type="text" id="title" v-model="recipe.title" required>
        </div>
        
        <div class="form-group">
          <label for="cookingTime">Cooking Time (minutes):</label>
          <input type="number" id="cookingTime" v-model="recipe.cookingTime" required>
        </div>
        
        <div class="form-group">
          <label for="imageUrl">Image URL:</label>
          <input type="text" id="imageUrl" v-model="recipe.imageUrl">
        </div>
        
        <div class="form-group">
            <label for="imageUrl">Image:</label>
            <div class="image-upload-container">
                <input type="text" id="imageUrl" class="image-url-input" v-model="imageUrl" placeholder="Enter Image URL" :disabled="isImageUploadSelected">
                <button class="toggle-button" @click="toggleImageSource">Choose Image</button>
            </div>
        </div>
        
        <div class="form-group">
          <label for="isVegan">Vegan:</label>
          <input type="checkbox" id="isVegan" v-model="recipe.isVegan">
        </div>
        
        <div class="form-group">
          <label for="isVegetarian">Vegetarian:</label>
          <input type="checkbox" id="isVegetarian" v-model="recipe.isVegetarian">
        </div>
        
        <div class="form-group">
          <label for="isGlutenFree">Gluten Free:</label>
          <input type="checkbox" id="isGlutenFree" v-model="recipe.isGlutenFree">
        </div>
        
        <div class="form-group">
          <label for="servingSize">Serving Size:</label>
          <input type="number" id="servingSize" v-model="recipe.servingSize" required>
        </div>
        
        <div class="form-group">
          <label for="instructions">Instructions:</label>
          <textarea id="instructions" v-model="recipe.instructions" required></textarea>
        </div>
        
        <div class="form-group">
          <label for="ingredients">Ingredients:</label>
          <textarea id="ingredients" v-model="recipe.ingredients" required></textarea>
        </div>
        
        <button type="submit" class="btn-submit">Add Recipe</button>
      </form>
    </div>
  </template>
  
  <script>
  export default {
    name: 'addRecipe',
    data() {
      return {
        recipe: {
          title: '',
          cookingTime: null,
          imageUrl: '',
          isVegan: false,
          isVegetarian: false,
          isGlutenFree: false,
          servingSize: null,
          instructions: '',
          ingredients: ''
        }
      };
    },
    methods: {
      submitForm() {
        // Here you can handle the form submission, e.g., send the data to an API or perform any required actions
        console.log(this.recipe);
        // Reset the form after submission
        this.resetForm();
      },
      resetForm() {
        // Reset the recipe object to clear the form inputs
        this.recipe = {
          title: '',
          cookingTime: null,
          imageUrl: '',
          isVegan: false,
          isVegetarian: false,
          isGlutenFree: false,
          servingSize: null,
          instructions: '',
          ingredients: ''
        };
      },
      handleImageUpload(event) {
        // Handle image upload logic here, e.g., store the uploaded image and update the image URL
        // You can access the uploaded file using `event.target.files[0]`
        console.log('Image uploaded:', event.target.files[0]);
      },
      toggleImageSource() {
      this.isImageUploadSelected = !this.isImageUploadSelected;
        },
    }
  };
  </script>
  
  <style>
  .container {
    max-width: 600px;
    margin: 0 auto;
    padding: 20px;
  }
  
  .title {
    text-align: center;
  }
  
  .form {
    display: grid;
    grid-gap: 10px;
  }
  
  .form-group {
    display: grid;
    grid-template-columns: 100px 1fr;
    align-items: center;
  }
  
  label {
    font-weight: bold;
  }
  
  .btn-submit {
    margin-top: 20px;
    padding: 10px 20px;
    background-color: #4CAF50;
    color: #fff;
    border: none;
    border-radius: 4px;
    cursor: pointer;
  }
  
  .btn-submit:hover {
    background-color: #45a049;
  }
  
  input[type="text"],
  input[type="number"],
  textarea {
    width: 100%;
    padding: 5px;
    border: 1px solid #ccc;
    border-radius: 4px;
    box-sizing: border-box;
  }
  
  input[type="file"] {
    display: none;
  }


  
.upload-container {
  display: flex;
  align-items: center;
}

.image-input {
  display: none;
}

.upload-button {
  padding: 10px 20px;
  background-color: #4CAF50;
  color: #fff;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}

.upload-button:hover {
  background-color: #45a049;
}

.image-upload-container {
  display: flex;
  align-items: center;
}

.image-url-input {
  flex: 1;
  margin-right: 10px;
}

.toggle-button {
  padding: 10px 20px;
  background-color: #4CAF50;
  color: #fff;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}

.toggle-button:hover {
  background-color: #45a049;
}

  </style>
  