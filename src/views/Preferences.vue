<template>
  <div class="container">
    <b-card border-variant="dark" header="PREFERENCES">
      <div>
       <b-card-body>
          <div class="bg-secondary text-light">
              <b-card-text>{{ text1 }}</b-card-text>
          </div>
        </b-card-body>
        <ul>
          <li v-for="item in invisibleItems" :key="item.route">
            {{ item.title }}
            <button variant="success" size="sm" @click="restoreItem(item)">(+) Add to menu</button>
          </li>
        </ul>
      </div>
    </b-card>
  </div>
</template>

<script>
import menubar from "../data/menubar.json";

export default {
  data() {
    return {
      items: [],
      text1: `User will have various menu items to access different pages and they will have the option to hide/show menu items as per their preference (2.5) `,
    };
  },
  computed: {
    invisibleItems() {
      return this.items.filter((item) => !item.visible);
    },
  },
  methods: {
    restoreItem(item) {
      item.visible = true; // Riaggiungi l'elemento impostando visible su true
      this.updateUserPreferencesInLocalStorage(); // Aggiorna userPreferences in localStorage
      this.updateItemsFromLocalStorage(); // Aggiorna this.items dai dati di localStorage
      location.reload();
       // Utilizza $parent per accedere al componente padre
      //this.$forceUpdate();
    },
    updateUserPreferencesInLocalStorage() {
      // Aggiorna userPreferences in localStorage
      if (this.items) {
        const userPreferences = this.items.reduce((prefs, item) => {
          prefs[item.route] = item.visible;
          return prefs;
        }, {});
        localStorage.setItem("userPreferences", JSON.stringify(userPreferences));
      }
    },
    updateItemsFromLocalStorage() {
      // Aggiorna this.items dai dati di localStorage
      const userPreferences = JSON.parse(localStorage.getItem("userPreferences")) || {};
      this.items = menubar.items.map((item) => ({
        ...item,
        visible: userPreferences[item.route] !== false,
      }));
    },
  },
  created() {
    // Inizializza this.items dai dati di localStorage
    this.updateItemsFromLocalStorage();
  },
};
</script>
