<template>
  <div class="container">
    <template>
  <div class="container">
    <b-card border-variant="dark" header="PREFERENCES">
      <!-- ... il resto del tuo codice ... -->
      <div class="form-check">
         <input type="checkbox" id="page1Checkbox" v-model="isPage1Visible" @change="updatePage1Visibility" />
        <label for="page1Checkbox">Show PAGE1</label>
      </div>
    </b-card>
  </div>
</template>
  </div>
</template>

<script>


export default {
  data() {
    return {
      isPage1Visible: true,
      text1: `User will have various menu items to access different pages and they will have the option to hide/show menu items as per their preference (2.5) `,
    };
  },
  computed: {
  
  },
  methods: {
    updatePage1Visibility() {
      console.log("1");
      this.$emit("update-page1-visibility", this.isPage1Visible);
    },
  },
  created() {
 
  },
};
</script>
