<template>
  <div id="app">
    <div>
      <b-nav tabs align="center" id="custom-nav">
        <b-nav-item>
          <router-link v-if="!isAuthenticated" to="/">LOGIN</router-link>
        </b-nav-item>
        <b-nav-item>
          <router-link v-if="!isAuthenticated" to="/register">REGISTER</router-link>
        </b-nav-item>
        <b-nav-item>
          <router-link v-if="isAuthenticated" to="/dashboard">DASHBOARD</router-link>
        </b-nav-item>
         <b-nav-item>
          <router-link v-if="isAuthenticated" to="/preferences">PREFERENCES</router-link>
        </b-nav-item>
        
        <!-- Dynamic Menu Items -->
        
          <div v-for="item in visibleItems" :key="item.route">
            <b-nav-item >
              <router-link v-if="isAuthenticated" :to="item.route">{{ item.title }} </router-link>
              <b-button v-if="isAuthenticated" @click="updateUserPreference(item)" v-model="item.visible" variant="danger" size="sm">X</b-button>
            </b-nav-item>
          </div>
       
        
        <button v-if="isAuthenticated" @click="logout">Logout</button>
      </b-nav>
    </div>
    <router-view />
  </div>
</template>

<script>
import menubar from "../data/menubar.json";

export default {
  props: {
    isAuthenticated: Boolean,
    logout: Function,
  },
  data() {
    return {
      items: menubar.items,
    };
  },
  computed: {
    visibleItems() {
      return this.items.filter((item) => item.visible);
    },
  },
  methods: {
    updateUserPreference(item) {
      // Toggle the visibility of the clicked item
      item.visible = !item.visible;
      // Update user preferences in localStorage
      const userPreferences = this.items.reduce((prefs, item) => {
        prefs[item.route] = item.visible;
        return prefs;
      }, {});
      localStorage.setItem("userPreferences", JSON.stringify(userPreferences));
    },
  },
  created() {
    const userPreferences = JSON.parse(localStorage.getItem("userPreferences")) || {};
    // Initialize the items based on user preferences in localStorage
    this.items = menubar.items.map((item) => ({
      ...item,
      visible: userPreferences[item.route] !== false,
    }));
  },
};
</script>

<style scoped>
.border {
  border: 2px dashed orange;
}
</style>
