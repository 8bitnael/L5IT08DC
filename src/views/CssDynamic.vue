<template>
  <div>
    <h1>Dynamic CSS in Vue</h1>

    <!-- Esempio 1: Stile dinamico basato su una condizione -->
    <div :style="{ color: isRed ? 'red' : 'blue' }">
      Questo testo cambia colore in base a "isRed"
    </div>
    <button @click="toggleColor">Cambia colore</button>

    <!-- Esempio 2: Stile dinamico con classi condizionali -->
    <div :class="{ active: isActive, disabled: isDisabled }">
      Questo elemento ha classi condizionali
    </div>
    <button @click="toggleClasses">Cambia classi</button>

    <!-- Esempio 3: Stile dinamico basato su dati del componente -->
    <div :style="customStyle">
      Questo elemento ha uno stile personalizzato
    </div>
    <button @click="changeCustomStyle">Cambia stile personalizzato</button>



      <div>
    <h1>Cambia il Colore di Sfondo</h1>
    <div :style="{ backgroundColor: backgroundColor }">
      Questo è un div con uno sfondo dinamico
    </div>
    <input type="color" v-model="backgroundColor" @input="changeBackgroundColor" />
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
      backgroundColor: '#ff0000', // Colore di sfondo iniziale (rosso)
      customStyle: {
        backgroundColor: 'yellow',
        fontSize: '20px',
        padding: '10px',
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
        backgroundColor: 'green',
        color: 'white',
        fontSize: '24px',
        padding: '12px',
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
