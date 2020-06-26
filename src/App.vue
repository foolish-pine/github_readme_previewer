<template>
  <v-app>
    <v-app-bar app flat dark color="blue-grey">
      <v-toolbar-title class="app-title"># GitHub README Previewer</v-toolbar-title>
    </v-app-bar>
    <MarkdownCompiler />
  </v-app>
</template>

<script lang="ts">
import { Vue, Component } from "vue-property-decorator";
import MarkdownCompiler from "./components/MarkdownCompiler.vue";

@Component({
  components: {
    MarkdownCompiler
  }
})
export default class App extends Vue {}
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