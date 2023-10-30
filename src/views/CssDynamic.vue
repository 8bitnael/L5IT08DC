<template>
  <div>
    <h1>Dynamic CSS in Vue</h1>

    <!-- Esempio 1: Stile dinamico basato su una condizione -->
    <div :style="{ color: isRed ? 'red' : 'blue' }">
      This text changes color based on "isRed"
    </div>
    <button @click="toggleColor">Change colour</button>

    <!-- Esempio 2: Stile dinamico con classi condizionali -->
    <div :class="{ active: isActive, disabled: isDisabled }">
      This element has conditional classes
    </div>
    <button @click="toggleClasses">Change classes</button>

    <!-- Esempio 3: Stile dinamico basato su dati del componente -->
    <div :style="customStyle">This element has a custom style</div>
    <button @click="changeCustomStyle">Change custom style</button>

    <div>
      <h1>Change the Background Color</h1>
      <div :style="{ backgroundColor: backgroundColor }">
        This is a div with a dynamic background
      </div>
      <input
        type="color"
        v-model="backgroundColor"
        @input="changeBackgroundColor"
      />
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      isRed: true,
      isActive: false,
      isDisabled: true,
      backgroundColor: "#ff0000", // Colore di sfondo iniziale (rosso)
      customStyle: {
        backgroundColor: "yellow",
        fontSize: "20px",
        padding: "10px",
      },
    };
  },
  methods: {
    toggleColor() {
      this.isRed = !this.isRed;
    },
    toggleClasses() {
      this.isActive = !this.isActive;
      this.isDisabled = !this.isDisabled;
    },
    changeCustomStyle() {
      this.customStyle = {
        backgroundColor: "green",
        color: "white",
        fontSize: "24px",
        padding: "12px",
      };
    },
    changeBackgroundColor() {
      // Questo metodo verrà chiamato quando l'utente seleziona un nuovo colore
      // dal selettore di colore
    },
  },
};
</script>

<style scoped>
/* Aggiungi stili CSS per le classi condizionali */
.active {
  background-color: lightblue;
}

.disabled {
  opacity: 0.5;
}
</style>
