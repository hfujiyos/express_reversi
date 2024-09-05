# VSCode

## ショートカット

- command + / : コメントアウト/イン
- command + N : ファイル新規
- command + J : ターミナル新規
- command + K : ターミナルクリア
- shift + command + V : マークダウンプレビュー
- shift + option + クリック : 複数カーソル
- shift + option + P : SwaggerUI表示

## 拡張機能

- Japanese Language Pack for Visual Studio Code ｜ Microsoft
- Git Graph ｜ mhutchie
- vscode-icons ｜ VSCode Icons Team
- Prettier - Code formatter ｜ Prettier
- ES7+ React/Redux/React-Native snippets ｜ dsznajder
- Nextjs snippets
- Jest ｜ Orta
- Playwright Test for VSCode
- YAML
- Swagger Viewer
- Mermaid Markdown Syntax Highlighting
- Draw.io Integration ｜ Henning Dieterichs

## settings.json

VSCode のメニューバーから、[基本設定] - [設定] にて設定画面を開きます
右上のアイコンの[設定 (JSON) を開く]をクリック
個人設定となる settings.json ファイルを設定します

```json
{
  //ｽﾀｲﾙ関連
  "workbench.iconTheme": "vscode-icons",
  "terminal.integrated.fontSize": 18,
  "editor.fontSize": 18,
  "editor.tabSize": 4,
  "editor.fontFamily": "Ricty Diminished",
  "editor.renderLineHighlight": "gutter",
  // 括弧記号色付け機能をON
  "editor.guides.bracketPairs": true,
  "editor.bracketPairColorization.enabled": true,
  // 信頼されたﾜｰｸｽﾍﾟｰｽで信頼されていないﾌｧｲﾙを開くときの設定
  "security.workspace.trust.untrustedFiles": "open",
  // ﾘﾓｰﾄﾘﾎﾟｼﾞﾄﾘの自動ﾌｪｯﾁをON
  "git.autofetch": true,
  // ﾌｧｲﾙ自動保存設定をOFF
  "files.autoSave": "off",
  // 行の自動折り返しをOFF
  "editor.wordWrap": "off",
  // Prettier個別設定を.prettierrc設定ﾌｧｲﾙからの読込をON（共通設定となるpackage.jsonよりもprettierrcを優先読込）
  "prettier.requireConfig": true,
  // ﾌｫｰﾏｯﾀをprettierに設定
  "editor.defaultFormatter": "esbenp.prettier-vscode",
  // ﾌｫｰﾏｯﾀをﾌｧｲﾙ保存時実行をON
  "editor.formatOnSave": true,
  // ﾏｰｸﾀﾞｳﾝ時のﾌｫｰﾏｯﾀをﾌｧｲﾙ保存時実行をON
  "[markdown]": { "editor.formatOnSave": true },
  // ﾏｰｸﾀﾞｳﾝ時の改行認識設定
  "markdown.preview.breaks": true,
  "workbench.startupEditor": "none",
  "hediet.vscode-drawio.resizeImages": null,
  "hediet.vscode-drawio.theme": "Kennedy",
  "vsicons.dontShowNewVersionMessage": true,
  "github.copilot.editor.enableAutoCompletions": true
}
```
