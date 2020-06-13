<template>
  <v-app>
    <v-app-bar app flat dark color="blue-grey ">
      <v-toolbar-title class="app-title"># GitHub README Previewer</v-toolbar-title>
    </v-app-bar>
    <InputDisplay />
  </v-app>
</template>

<script lang="ts">
import Vue from "vue";
import InputDisplay from "./components/InputDisplay.vue";

export default Vue.extend({
  name: "App",

  components: {
    InputDisplay
  },

  data: () => ({
    //
  })
});
</script>

<style lang="scss">
// Web Fontのちらつき対策
html {
  visibility: hidden;
}
html.wf-active,
html.loading-delay {
  visibility: visible;
}
.app-title {
  font-family: "Oswald", sans-serif;
  font-size: 2rem !important;
}
</style>