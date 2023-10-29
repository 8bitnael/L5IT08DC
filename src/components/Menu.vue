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
    isAuthenticated: Boolean, // Dichiarazione della prop isAuthenticated
    logout: Function,
  },
  data() {
    return {
      model: 1,
      name: "Menu",
      items: menubar.items,
    }
  }
}
</script>
<style scoped>
.border {
  border: 2px dashed orange;
}
</style>