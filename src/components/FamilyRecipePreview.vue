<template>
    <b-card class="recipe-preview">
      <div class="recipe-body">
        <div :title="recipe.title" class="recipe-title" @click="goToRecipe">{{ recipe.title }}</div>
  <div class="recipe-image-container" @click="goToRecipe">

  <div v-if="!imageLoaded" class="spinner">
    <div class="spinner-border text-success" role="status">
      <span class="sr-only">Loading...</span>
    </div>
  </div>
  <img
    :src="recipe.image"
    alt="Recipe"
    class="recipe-image"
    @load="handleImageLoad"
  />
  
</div>
</div>
<div class="recipe-footer">
  <ul class="recipe-overview">
    <li>{{ recipe.readyInMinutes }} minutes</li>
    <li>{{ recipe.popularity }} likes</li>
  </ul>
</div>
</b-card>
</template>


<script>

export default {
name: "FamilyRecipePreview",

data() {
return {
imageLoaded: false,
isFavorite: this.recipe.isFavorite

};
},
computed: {
isLoggedIn() {
return localStorage.getItem("isLoggedIn") === "true";
},
},




methods: {
goToRecipe() {
console.log("goToRecipe", this.recipe.id);
this.$router.push({ name: "recipe", params: { recipeId: this.recipe.id } });
},
handleImageLoad() {
this.imageLoaded = true;
console.log(this.recipe);
},

async toggleFavorite() {
if (this.$root.store.username && !this.isFavorite) {
this.recipe.isFavorite = !this.recipe.isFavorite;
this.isFavorite = true;
try {
await this.axios.post(
  this.$root.store.server_domain + "/users/favorites",
  { recipeId: this.recipe.id }
);
this.$emit("favorite-updated", this.recipe); // Emit the event
} catch (error) {
this.$root.toast("Input Error", error.message, "danger");
}
}
},

},



props: {
recipe: {
type: Object,
required: true
}

}
};
</script>

<style scoped>

.recipe-preview {
margin: 3%;
color: black;
background: linear-gradient(
to right,
rgba(255, 255, 255, 0.1),
rgba(141, 184, 133, 0.1),
rgba(99, 158, 88, 0.1)
);
border-radius: 10px;
border: none;
width: 70%;
box-shadow: 0 0 10px rgba(0, 0, 0, 0.3);
transition: 0.3s;
}

.recipe-preview:hover {
box-shadow: 0 0 20px rgba(0, 0, 0, 0.5);
}

.recipe-preview > .recipe-body {
padding: 10px;
width: 100%;
height: auto;
position: relative;
text-align: left;
white-space: nowrap;
overflow: hidden;
text-overflow: ellipsis;
}

.recipe-preview .recipe-image-container {
position: relative;
height: 200px;
}

.middle {
transition: .5s ease;
opacity: 0;
position: absolute;
top: 50%;
left: 50%;
transform: translate(-50%, -50%);
-ms-transform: translate(-50%, -50%);
text-align: center;
}
.recipe-preview .recipe-body .recipe-image {
margin: auto;
display: block;
width: 80%;
height: 80%;
-webkit-background-size: cover;
-moz-background-size: cover;
background-size: cover;
border-radius: 10px;
left: 0;
opacity: 1;
transition: .5s ease;
backface-visibility: hidden;
cursor: pointer;
}
.recipe-preview .recipe-body:hover .recipe-image {
opacity: 0.3;
}


.recipe-footer {
width: 100%;
height: 50%;
overflow: hidden;
}

.recipe-footer .recipe-title {
padding: 10px;
width: 100%;
font-size: 12pt;
text-align: left;
white-space: nowrap;
overflow: hidden;
text-overflow: ellipsis;
}

.recipe-footer ul.recipe-overview {
padding: 5px 10px;
width: 100%;
display: flex;
justify-content: space-between;
list-style-type: none;
margin-bottom: 0;
}

.recipe-footer ul.recipe-overview li {
flex-grow: 1;
width: 90px;
text-align: center;
}

</style>
