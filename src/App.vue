<template>
  <div id="app">
    <Menu :isAuthenticated="isAuthenticated" :logout="logout"/>
  </div>
</template>

<script>
import firebase from "firebase";
import Vue from "vue";
import modal from "../src/components/Modal.vue";
import Menu from "./components/Menu.vue";

export default {
  components: {
    Menu, // Aggiungi il tuo componente Men
  },
  data() {
    return {
      isAuthenticated: false,
      items: [], // Inizializza un array vuoto per i menu items
    };
  },
  created() {
    // Controlla lo stato di autenticazione all'avvio dell'applicazione
    firebase.auth().onAuthStateChanged((user) => {
      this.isAuthenticated = user !== null;
    });
  },
  mounted() {},
  methods: {
    logout() {
      firebase
        .auth()
        .signOut()
        .then(() => {
          //alert('Successfully logged out');
          const modalComponent = new Vue(modal);
          modalComponent.$mount();
          modalComponent.showModal(
            "Authentication",
            "Successfully logged out!"
          );
          localStorage.removeItem("uuid");
          this.$router.push("/");
        })
        .catch((error) => {
          alert(error.message);
          this.$router.push("/");
        });
    },
  },
};
</script>
<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

#nav {
  padding: 30px;
}

#nav a {
  font-weight: bold;
  color: #2c3e50;
}

#nav a.router-link-exact-active {
  color: #42b983;
}

input {
  margin-right: 20px;
}

#custom-nav {
  background-color: black; /* Sostituisci con il colore desiderato */
  color: slategrey; /* Cambia il colore del testo se necessario */
}
</style>
