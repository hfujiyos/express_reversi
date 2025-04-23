# vscode-js-debug

- React.js の場合は CSR をデバッグします。Next.js の場合は SSR をデバッグします。
- 上記のため、VSCode の launch.json にてデバッガをアタッチするポート番号に注意します。
- 最新のデバッガは `pwa-chrome` ですが、 `chrome` でも問題ありません

## React.js を VSCode でデバッグする

### ステップ１ VSCode のデバッガを設定する

- VS Code 側（.vscode/task.json）の設定ファイルを作成します。

  ```sh
  $ mkdir .vscode
  $ touch .vscode/task.json
  ```

  ```json:.vscode/task.json
  {
      "version": "2.0.0",
      "tasks": [
          {
              "type": "npm",
              "script": "start",
              "label": "npm: start",
              "detail": "react-scripts start",
              "group": {
                  "kind": "test",
                  "isDefault": true
              },
              "isBackground": true,
              "problemMatcher": {
                  "owner": "custom",
                  "pattern": {
                      "regexp": "ˆ$"
                  },
                  "background": {
                      "activeOnStart": true,
                      "beginsPattern": "Compiling...",
                      "endsPattern": "Compiled .*"
                  }
              }
          }
      ]
  }
  ```

- VS Code 側（.env）の設定ファイルを作成します。このままタスクを実行してもよいのですが、初回起動時に自動的にデバッグとは関係ないブラウザが表示されてしまいます。ここでの操作はデバッグに影響せず、ブレークポイントやウォッチ式が効かないので注意が必要です。そこで、 react-scripts start 実行時にブラウザの自動表示を抑制する設定を行います。

  ```sh
  $ touch .vscode/launch.json
  ```

  ```sh:.env
  BROWSER=none
  ```

- VS Code 側（.vscode/launch.json）の設定ファイルを作成します。

  ```sh
  $ touch .vscode/launch.json
  ```

  ```json:.vscode/launch.json
  {
      "version": "0.2.0",
      "configurations": [
          {
              "type": "chrome",
              "request": "launch",
              "preLaunchTask": "npm: start",
              "name": "Launch Chrome against localhost",
              "url": "http://localhost:3000",
              "webRoot": "${workspaceFolder}",
              "sourceMaps": true,
              "sourceMapPathOverrides": {
                  "webpack:///./*": "${webRoot}/src/*"
              }
          },
      ]
  }
  ```

### ステップ２ デバッグの開始

- VSCode 上で F5 キーを押すと、デバッグが開始されます。

- なお、launch.json に複数の構成を定義している場合は、デバッグ画面で左上部のドロップダウンリストから Launch Chrome against localhost を選択してからデバッグを開始してください。

- デバッグが開始されると、まずターミナル上で preLaunchTask で指定した npm: start タスクが実行されます。このタスクは実質的には react-scripts start を実行します。

- その後、GoogleChrome が自動的に起動します。ここで起動したブラウザがデバッグ対象となり、ここで実際にアプリを操作しながら、VSCode 上でブレークポイントを設定したり、ウォッチ式で変数の監視ができるようになります。

## 参考文献

- [【React.js】VSCode+GoogleChrome で React のデバッグを行う](https://zenn.dev/rhene/articles/setup-vscode-to-react-debug)
