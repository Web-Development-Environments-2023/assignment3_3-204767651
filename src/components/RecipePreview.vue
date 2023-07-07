      <template>
        <!-- <router-link :to="{ name: 'recipe', params: { recipeId: recipe.id } }"> -->
          <b-card class="recipe-preview">
            <div class="recipe-body">
              <div :title="recipe.title" class="recipe-title" @click="goToRecipe">{{ recipe.title }}</div>
              <div class="recipe-image-container" @click="goToRecipe">
                <img
                  img-alt="Recipe"
                  :src="recipe.image"
                  class="recipe-image"

        />
      </div>
      </div>
      <div class="recipe-footer">
        <ul class="recipe-overview">
          <li>{{ recipe.readyInMinutes }} minutes</li>
          <li>{{ recipe.aggregateLikes }} likes</li>
          <li>{{ recipe.servings ? recipe.servings + " servings" : "" }} </li>
          <li v-if="recipe.vegetarian"><i class="fas fa-leaf"></i></li>
          <li v-if="recipe.vegan"><i class="fas fa-seedling" style = "color: rgb(15, 143, 68)"></i></li>
          <li v-if="recipe.isWatched"><i class="fas fa-eye"></i></li>
          <li v-if="this.$root.store.username">
            <button
              @click="toggleFavorite()"
              class="btn btn-link"
              style="padding: 0; border: none; background: none;"
            >
              <i
                v-if="this.isFavorite"
                class="fas fa-heart"
                style="color: rgb(15, 143, 68);"
              ></i>
              <i
                v-else
                class="far fa-heart"
                style="color: rgb(0, 0, 0);"
              ></i>
            </button>


          </li>


        </ul>
      </div>
    </b-card>
  <!-- </router-link> -->
</template>


<script>

export default {
  name: "RecipePreview",
  mounted() {
    // this.axios.get(this.recipe.image).then((i) => {
    //   this.image_load = true;
    // });
    // this.isFavorite = this.recipe.isFavorite;
  },
  data() {
    return {
      // image_load: false,
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
  /* display: inline-block;
  width: 90%;
  height: 90%; */
  position: relative;
  margin: 3%;
  color:black;
  background: linear-gradient(to right,rgba(255, 255, 255, 0.1), rgba(141, 184, 133, 0.1), rgba(99, 158, 88, 0.1));
  border-radius: 10px;
  border: none;
  width: 70%;
  height: 1000%;
  
}
.recipe-preview > .recipe-body {
  padding: 10px 10px;
  width: 100%;
  height: auto;
  position: relative;
  text-align: left;
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
  left: 0;
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

.recipe-preview .recipe-body:hover .recipe-image {
  opacity: 0.3;
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

.recipe-preview .recipe-footer {
  width: 100%;
  height: 50%;
  overflow: hidden;
}

.recipe-preview .recipe-footer .recipe-title {
  padding: 10px 10px;
  width: 100%;
  font-size: 12pt;
  text-align: left;
  white-space: nowrap;
  overflow: hidden;
  -o-text-overflow: ellipsis;
  text-overflow: ellipsis;

}

.recipe-preview .recipe-footer ul.recipe-overview {
  padding: 5px 10px;
  width: 100%;
  display: -webkit-box;
  display: -moz-box;
  display: -webkit-flex;
  display: -ms-flexbox;
  display: flex;
  -webkit-box-flex: 1;
  -moz-box-flex: 1;
  -o-box-flex: 1;
  box-flex: 1;
  -webkit-flex: 1 auto;
  -ms-flex: 1 auto;
  flex: 1 auto;
  table-layout: fixed;
  margin-bottom: 0px;
}

.recipe-preview .recipe-footer ul.recipe-overview li {
  -webkit-box-flex: 1;
  -moz-box-flex: 1;
  -o-box-flex: 1;
  -ms-box-flex: 1;
  box-flex: 1;
  -webkit-flex-grow: 1;
  flex-grow: 1;
  width: 90px;
  display: table-cell;
  text-align: center;
}

@import "~@fortawesome/fontawesome-free/css/all.css";
</style>
