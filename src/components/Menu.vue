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
         <b-nav-item>
          <router-link v-if="isAuthenticated" to="/cssdynamic">DYNAMIC CSS</router-link>
        </b-nav-item>
        
        <!-- Dynamic Menu Items -->
        <b-nav-item>
          <router-link v-if="isAuthenticated && isPage1Visible"   to="/page1">PAGE1</router-link>
        </b-nav-item>
         <b-nav-item>
          <router-link v-if="isAuthenticated && isPage2Visible"   to="/page2">PAGE2</router-link>
        </b-nav-item>
       
      
        <button v-if="isAuthenticated" @click="logout">Logout</button>
      </b-nav>
    </div>
    <router-view @update-page-visibility="updatePageVisibility" />
  </div>
</template>

<script>
 

export default {
  name: "Menu",
  props: {
    isAuthenticated: Boolean,
    logout: Function,
  },
  data() {
    return {
        isPage1Visible: true,
        isPage2Visible: true,
    };
  },
  computed: {
    
  },
  methods: {
    updatePageVisibility(isPage1Visible, isPage2Visible) {
      this.isPage1Visible = isPage1Visible;
      this.isPage2Visible = isPage2Visible;
    },
  },
  created() {
    console.log("2");
    this.$on("update-page1-visibility", this.updatePage1Visibility);
  },
};
</script>

<style scoped>
.border {
  border: 2px dashed orange;
}
</style>
