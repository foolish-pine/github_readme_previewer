<template>
  <v-container class="pt-5">
    <v-content>
      <div class="d-flex mb-2">
        <!-- ローカルファイル読み込み用のinput（非表示） -->
        <input style="display: none;" ref="loadFile" type="file" accept=".md" @change="loadFile" />
        <v-btn class="mr-5" small @click="clickFileLoadButton">
          <v-icon class="mr-2">mdi-folder-open</v-icon>Open File
        </v-btn>

        <v-dialog v-model="saveFileDialog" max-width="500px">
          <template v-slot:activator="{ on }">
            <v-btn class="mr-5" small v-on="on">
              <v-icon class="mr-2">mdi-content-save</v-icon>Save File
            </v-btn>
          </template>
          <v-card class="py-5">
            <v-card-title>
              <span class="sutitle-1">ファイル名を入力して保存します</span>
            </v-card-title>
            <v-card-text>
              <v-text-field v-model="fileName" suffix=".md" required></v-text-field>
            </v-card-text>
            <v-card-actions>
              <v-spacer></v-spacer>
              <v-btn color="grey darken-1" text @click="saveFileDialog = false">キャンセル</v-btn>
              <v-btn color="blue darken-1" text @click="saveFile">保存する</v-btn>
            </v-card-actions>
          </v-card>
        </v-dialog>

        <v-btn class="mr-5" small @click="copyText">
          <v-icon class="mr-2">mdi-content-copy</v-icon>Copy To Clipboard
        </v-btn>
        <v-btn color="error" small @click="clearText">
          <v-icon class="mr-2">mdi-delete</v-icon>Clear
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
  saveFileDialog = false;
  fileName = "";
  markdownText = "### こちらにMarkdown記法で記述してください。";

  $refs!: {
    loadFile: HTMLFormElement;
  };

  // テキストエリアの内容をクリップボードにコピーする
  copyText(): void {
    document.getElementsByTagName("textarea")[0].select();
    document.execCommand("copy");
  }

  clearText(): void {
    this.markdownText = "";
  }

  // ローカルファイルをテキストとして読み込み、テキストエリアに表示する
  loadFile(): void {
    const file = this.$refs.loadFile.files[0];
    if (!file) {
      return;
    }
    const reader = new FileReader();
    reader.addEventListener("load", () => {
      this.markdownText = String(reader.result);
    });
    reader.readAsText(file);
  }

  // Open Fileボタンクリック時にloadFileを呼び出す
  clickFileLoadButton(): void {
    this.$refs.loadFile.click();
  }

  // ダイアログのテキストフィールドに入力した名前でファイルを保存する
  saveFile(): void {
    const blob = new Blob([this.markdownText], { type: "text/.md" });
    const link = document.createElement("a");
    link.href = URL.createObjectURL(blob);
    link.download = `${this.fileName}.md`;
    link.style.display = "none";
    document.body.appendChild(link);

    link.click();
    document.body.removeChild(link);
    this.saveFileDialog = false;
    this.fileName = "";
  }

  // MarkdownをHTMLに変換する
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