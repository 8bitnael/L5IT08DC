<template>
  <div class="container">
    <template>
  <div class="container">
    <b-card border-variant="dark" header="PREFERENCES">
      <!-- ... il resto del tuo codice ... -->
      <div class="form-check">
         <input type="checkbox" v-model="isPage1Visible" @change="updatePageVisibility" />
        <label for="page1">Show Page 1</label>
      </div>

        <div class="form-check">
          <input type="checkbox" v-model="isPage2Visible" @change="updatePageVisibility" />
          <label for="page2">Show Page 2</label>
        </div>
    </b-card>
  </div>
</template>
  </div>
</template>

<script>


export default {
  name: "Preferences",
  props: {
    //isPage1Visible: Boolean,
    //isPage2Visible: Boolean,
  },
  data() {
    return {
      isPage1Visible: true,
      isPage2Visible: true,
      text1: `User will have various menu items to access different pages and they will have the option to hide/show menu items as per their preference (2.5) `,
    };
  },
  computed: {
  
  },
  methods: {
    updatePageVisibility() {
      this.$emit("update-page-visibility", this.isPage1Visible, this.isPage2Visible);
    },
  },
  created() {
 
  },
};
</script>
