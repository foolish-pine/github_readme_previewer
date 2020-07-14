# GitHub README用マークダウンエディタ『# GitHub README Previewer』

## デモ
<img src="https://user-images.githubusercontent.com/59694183/84570379-2855d680-adc8-11ea-8399-7a1275b077e0.gif" width="500">
<br>
<br>

[こちら](https://github-readme-previewer.netlify.app/)からお使いいただけます。

<br>
<br>

## ポイント
- TypeScript + Vue.jsで作成したマークダウンエディタです。
- テキストエリアにMarkdown形式で記述し、それをリアルタイムでプレビューできます。
- プレビュー画面のCSSには「github-markdown.css」を使用させていただきました。GitHubのREADME.mdそのままの見た目でプレビューできます。
- ローカルファイルを開いて内容をテキストエリアに表示できます。
- テキストエリアの入力内容を名前をつけて.md形式で保存することができます。
<br>

## 制作者コメント
「GitHubのREADME、あの画面に表示される見た目そのままでプレビューできたら便利じゃん？」と思ったのでつくってみました。markdownの解析はJavaScriptライブラリ『Marked』がやってくれており、CSSはGitHubのmarkdown用CSS『github-markdown.css』をそのまま使用しているので、制作者は実質何もしてません。TypeScriptの練習をしようと思いTSでコードを書くも、記述量がそもそも少ないのでたいした練習にもならなかったというオマケつきです。苦し紛れでローカルファイルのインポート機能や名前を付けて.md形式で保存する機能もつけてみました。もしよければ使ってみてください。
<br>
<br>

## 制作に使用した言語・ツール
TypeScript / Vue.js / Vuetify
<br>
<br>

## 制作時間
10時間
<br>
<br>
