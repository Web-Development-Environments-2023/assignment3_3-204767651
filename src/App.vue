<template>
  <div id="app">
    <div id="content">

   
    <!-- Navbar -->
    <div id="nav">
      <!-- Router Links -->
      <router-link :to="{ name: 'main' }">Main Page</router-link> |
      <router-link :to="{ name: 'search' }">Search</router-link> |
      <router-link :to="{ name: 'about' }">About</router-link> |
      
      <!-- Personal dropdown (visible if a username is available) -->
      <div id="personal-dropdown" v-if="$root.store.username" :class="{ active: isPersonalActive }">
        Personal |
        
        <!-- Dropdown content -->
        <div class="dropdown-content">
          <router-link :to="{ name: 'favorites' }">Favorites Recipes</router-link>
          <router-link :to="{ name: 'myrecipes' }">My Recipes</router-link>
          <router-link :to="{ name: 'familyrecipes' }">Family Recipes</router-link>
        </div>
      </div>
      
      <!-- Add Recipe button (visible if a username is available) -->
      <span v-if="$root.store.username">
        <!-- Button trigger modal -->
        <button type="button" id="modalBtn" class="btn btn-success" data-bs-toggle="modal" data-bs-target="#exampleModal">
        Add Recipe
        </button>
      </span>
      
      <!-- Add Recipe Modal -->
      <!-- Modal -->
      <div class="modal fade" id="exampleModal" tabindex="-1" aria-labelledby="exampleModalLabel" aria-hidden="true">
        <div class="modal-dialog">
          <div class="modal-content">
            <div class="modal-header">
              <h1 class="modal-title fs-5" id="exampleModalLabel">Add Recipe</h1>
              <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
            </div>
            <div class="modal-body">
              ...
            </div>
            <div class="modal-footer">
              <button type="button" class="btn btn-secondary" data-bs-dismiss="modal">Close</button>
              <button type="button" class="btn btn-success">Save changes</button>
            </div>
          </div>
        </div>
      </div>
      
      <!-- Guest and user sections -->
      <div id="reglog">
        <!-- Guest section -->
        <span v-if="!$root.store.username">
          <div id="guest">
            <h5 style="font-weight: bold;" >Hello Guest:</h5>
          </div>
          <div id="reglog-links">
            <router-link :to="{ name: 'register' }">Register</router-link> |
            <router-link :to="{ name: 'login' }">Login</router-link> |
          </div>
        </span>
        
        <!-- User section -->
        <span v-else>
          <div id="user">
            <span class="username">{{ $root.store.username }}</span>
            <button @click="logout" class="logout-button">Logout</button>
          </div>
        </span>
      </div>
    </div>
    
    <!-- Router View -->
    <router-view />

  </div>
    <!-- Footer -->
    <footer>
      <div class="footer_container">
        <!-- <p>Developed by </p>
      <span><i class="fab fa-github" href="https://github.com/idolou">Ido Lourie</i></span>  -->
      <p>Developed by <a href="https://github.com/idolou" target="_blank" rel="noopener noreferrer"><i class="fab fa-github"></i></a> Ido Lourie - <a href="https://github.com/EladShmulevich" target="_blank" rel="noopener noreferrer"><i class="fab fa-github"></i></a> Elad Shmulevich</p>
      </div>
    </footer>



  </div>
</template>

<script>
import AddRecipeModal from "./pages/AddRecipeModal.vue";

export default {
  name: "App",
  data() {
    return {
      showAddRecipeModal: false,
    };
  },
  computed: {
    isPersonalActive() {
      return (
        this.$route.name === "favorites" ||
        this.$route.name === "myrecipes" ||
        this.$route.name === "familyrecipes"
      );
    },
  },
  methods: {
    logout() {
      this.$root.store.logout();
      this.$root.isLoggedIn = false;
      this.$root.toast("Logout", "User logged out successfully", "success");
      localStorage.setItem("isLoggedIn", false);
      this.isLoggedIn = false;
      sessionStorage.clear();
      this.$router.push("/").catch(() => {
        this.$forceUpdate();
      });
    },
    openAddRecipeModal() {
      this.showAddRecipeModal = true;
      console.log("openAddRecipeModal");
      console.log(this.showAddRecipeModal);
    },
    closeAddRecipeModal() {
      this.showAddRecipeModal = false;
    },
  },
  components: {
    //AddRecipeModal,
  },
};
</script>

<style lang="scss">
@import "@/scss/form-style.scss";

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  font-size: 1em;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  min-height: 100vh;
  background: linear-gradient(to left,rgba(255, 255, 255), rgba(141, 184, 133, 0.5), rgba(99, 158, 88, 0.5));
  display: flex;
  flex-direction: column;
  
}

#nav {
  padding: 30px;
  border-bottom: 1px solid #ccc;
  // background: rgb(0, 172, 92);
  background: linear-gradient(90deg, rgb(105, 189, 150) 0%, rgba(0, 172, 92, 1) 35%, rgb(64, 156, 99) 100%);}

#nav a {
  font-weight: bold;
  color: #ffffff;
  transition: color 0.3s ease-in-out;
}

#nav a:hover {
  color: #4c687a;
}

#nav a.router-link-exact-active {
  color: #2c3e50;
}

#reglog {
  float: right;
  display: flex;
  align-items: center;
}

#reglog h5 {
  margin-right: 10px;
  font-weight: normal;
}

#reglog router-link {
  margin-right: 10px;
}

#reglog span {
  margin-right: 10px;
}

#personal-dropdown {
  position: relative;
  display: inline-block;
  margin-right: 10px;
  font-weight: bold;
  color: #ffffff;
  transition: color 0.3s ease-in-out;
}

#personal-dropdown:hover {
  color: #52768f;
  text-decoration: underline;
}

#personal-dropdown .dropdown-content {
  display: none;
  position: absolute;
  background-color: #f9f9f9;
  min-width: 160px;
  box-shadow: 0px 8px 16px 0px rgba(250, 248, 248, 0.2);
  padding: 12px 16px;
  z-index: 1;
}

#personal-dropdown:hover .dropdown-content {
  display: block;
  /* Add a delay before hiding the dropdown content */
  transition-delay: 0.3s;
} 

#personal-dropdown .dropdown-content a {
  color: black;
  padding: 12px 16px;
  text-decoration: none;
  display: block;
  transition: color 0.3s ease-in-out;
}

#personal-dropdown .dropdown-content a:hover {
  color: #43b680;
  text-decoration: underline;
}

#personal-dropdown .dropdown-content a.router-link-exact-active {
  color: #42b983;
  padding: 12px 16px;
  text-decoration: none;
  display: block;
}

#personal-dropdown.active {
  color: #2c3e50;
}

#guest {
  display: inline-block;
  font-weight: bold;
  font-size: 1.5em;
}

#reglog-links {
  display: inline-block;
  margin-left: 0.2em;
}

#user {
  display: inline-block;
  vertical-align: middle;
}

#modalBtn{
  background-color: #42b983;
  color: #fff;
  border: none;
  padding: 6px 10px;
  border-radius: 4px;
  cursor: pointer;
  transition: background-color 0.3s ease-in-out;
}

#modalBtn:hover {
  background-color: #1d9b51;
}

.username {
  font-weight: bold;
  margin-right: 10px;
}


.logout-button {
  background-color: #42b983;
  color: #fff;
  border: none;
  padding: 6px 10px;
  border-radius: 4px;
  cursor: pointer;
  transition: background-color 0.3s ease-in-out;
}

.logout-button:hover {
  background-color: #74797e;
}



#personal-dropdown .dropdown-content {
  /* Existing styles... */
  margin-top: 1px; /* Add a small margin to separate the dropdown from the parent */
}

#personal-dropdown .dropdown-content:hover {
  display: block;
  /* Cancel the transition delay when hovering over the dropdown content */
  transition-delay: 0s;
}

.modal {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background-color: rgba(0, 0, 0, 0.5);
  display: flex;
  align-items: center;
  justify-content: center;
  z-index: 999;
}

.modal-content {
  background-color: #fff;
  padding: 20px;
  max-width: 600px;
  margin: 0 auto;
  border-radius: 4px;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.3);
}

.modal-close {
  background-color: #ccc;
  color: #fff;
  border: none;
  padding: 6px 10px;
  border-radius: 4px;
  cursor: pointer;
  position: absolute;
  top: 10px;
  right: 10px;
}

.modal {
  display: none;
  position: fixed;
  z-index: 1050;
  left: 0;
  top: 0;
  width: 100%;
  height: 100%;
  overflow: hidden;
  outline: 0;
}

.modal-dialog {
  position: relative;
  width: auto;
  margin: 10px;
}

.modal-content {
  position: relative;
  display: flex;
  flex-direction: column;
  background-color: #fff;
  background-clip: padding-box;
  border: 1px solid rgba(0, 0, 0, 0.2);
  border-radius: 0.3rem;
  outline: 0;
}

.modal-header {
  padding: 15px;
  border-bottom: 1px solid #e9ecef;
}

.modal-title {
  margin-top: 0;
  margin-bottom: 0.5rem;
}

.modal-body {
  position: relative;
  flex: 1 1 auto;
  padding: 15px;
  overflow-y: auto;
}

.modal-footer {
  padding: 15px;
  border-top: 1px solid #e9ecef;
  display: flex;
  justify-content: flex-end;
}

.close {
  float: right;
  font-size: 1.5rem;
  font-weight: 700;
  line-height: 1;
  color: #000;
  text-shadow: 0 1px 0 #fff;
  opacity: 0.5;
}

.close:hover {
  color: #000;
  text-decoration: none;
  opacity: 0.75;
}
#content {
  flex-grow: 1;
}

footer {
  background: linear-gradient(to right,rgb(51, 134, 78), rgba(35, 126, 19, 0.5), rgba(20, 109, 150, 0.4));
  margin-top: auto;

  color: #ffffff;
  padding: 20px 0;
  text-align: center;
}

footer p {
  margin: 0;
}

footer i {
  vertical-align: middle;
}


footer a {
  color: #ffffff;
  text-decoration: none;
  margin: 0 5px;
}
</style>
