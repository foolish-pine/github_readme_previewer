<template>
  <v-container class="pt-5">
    <v-content>
      <div class="d-flex mb-1">
        <v-btn class="mr-5" small @click="copyText">
          <v-icon class="mr-2">mdi-content-copy</v-icon>Copy To Clipboard
        </v-btn>
        <v-btn color="error" small @click="deleteText">
          <v-icon class="mr-2">mdi-delete</v-icon>DELETE
        </v-btn>
      </div>
      <v-row class="textarea-container">
        <v-col cols="12" xs="12" md="6">
          <v-textarea v-model="markdownText" no-resize outlined height="100%"></v-textarea>
        </v-col>
        <v-col class="compiledTextarea" cols="12" xs="12" md="6">
          <div class="markdown-body" v-html="compiledMarkdown"></div>
        </v-col>
      </v-row>
    </v-content>
  </v-container>
</template>

<script lang="ts">
import Component from "vue-class-component";
import { Vue } from "vue-property-decorator";
import marked from "marked";

@Component
export default class MarkdownCompiler extends Vue {
  markdownText = "### こちらにMarkdown記法で記述してください。";

  copyText(): void {
    document.getElementsByTagName("textarea")[0].select();
    document.execCommand("copy");
  }

  deleteText(): void {
    this.markdownText = "";
  }

  get compiledMarkdown(): string {
    return marked(this.markdownText);
  }
}
</script>

<style lang="scss">
.v-main,
.v-main__wrap,
.container,
.v-textarea {
  height: 100%;
}
.button-container {
  height: 10%;
}
.textarea-container {
  height: 90%;
}
.v-input__control {
  height: 100% !important;
}
.markdown-body {
  height: 100%;
  max-height: 70vh;
  overflow-y: scroll;
}
.v-application code {
  background-color: #f6f8fa !important;
  color: unset !important;
}
</style>