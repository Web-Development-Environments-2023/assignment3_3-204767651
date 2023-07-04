<template>
  <div id="app">
    <div id="nav">
      <router-link :to="{ name: 'main' }">Main Page</router-link>|
      <router-link :to="{ name: 'search' }">Search</router-link>|
      <router-link :to="{ name: 'about' }">About</router-link>|
      <!-- {{ !$root.store.username }} -->
<div id="personal-dropdown" v-if="$root.store.username" :class="{ active: isPersonalActive }">
        Personal|
        <div class="dropdown-content">
          <router-link :to="{ name: 'favorites' }">Favorites Recipes</router-link>
          <router-link :to="{ name: 'myrecipes' }">My Recipes</router-link>
          <router-link :to="{ name: 'familyrecipes' }">Family Recipes</router-link>
        </div>
      </div>
      <span v-if="$root.store.username">
        <router-link :to="{ name: 'addrecipe' }">Add Recipe</router-link>
      </span>

      <!-- {{ !$root.store.username }} -->
      <div id="reglog">
        <span v-if="!$root.store.username">
          <!-- Guest: -->
          <div id="guest">
            <h5>Hello Guest:</h5>
          </div>
          <div id="reglog-links">
            <router-link :to="{ name: 'register' }">Register</router-link>|
            <router-link :to="{ name: 'login' }">Login</router-link>|
          </div>
        </span>
        <span v-else>
          <div id="user">
            <span class="username">{{ $root.store.username }}</span>
            <button @click="Logout" class="logout-button">Logout</button>
          </div>
        </span>
      </div>
    </div>
    <router-view />
  </div>
</template>


<script>
export default {
  name: "App",
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
    Logout() {
      this.$root.store.logout();
      this.$root.toast("Logout", "User logged out successfully", "success");
      localStorage.setItem("isLoggedIn", false);

      this.$router.push("/").catch(() => {
        this.$forceUpdate();
      });
    }
  }
};
</script>

<style lang="scss">
@import "@/scss/form-style.scss";

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  min-height: 100vh;
  background: linear-gradient(to left,rgba(255, 255, 255), rgba(141, 184, 133, 0.5), rgba(99, 158, 88, 0.5));
  
}

#nav {
  padding: 30px;
  border-bottom: 1px solid #ccc;
  background: rgb(0, 172, 92);
}

#nav a {
  font-weight: bold;
  color: #ffffff;
  transition: color 0.3s ease-in-out;
}

#nav a:hover {
  color: #0c99f7;
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
  color: #0c99f7;
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
  color: #0c99f7;
  text-decoration: underline;
}

#personal-dropdown .dropdown-content a.router-link-exact-active {
  color: #42b983;
  padding: 12px 16px;
  text-decoration: none;
  display: block;
}

#personal-dropdown.active {
  color: #42b983;
}

#guest {
  display: inline-block;
}

#reglog-links {
  display: inline-block;
  margin-left: 10px;
}

#user {
  display: inline-block;
  vertical-align: middle;
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


</style>
