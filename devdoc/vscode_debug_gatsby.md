# vscode-js-debug

- React.js の場合は CSR をデバッグします。Gatsby.js の場合は SSG をデバッグします。

## Gatsby.js を VSCode でデバッグする

- VS Code 側（.vscode/launch.json）の設定ファイルを作成します。

  ```sh
  $ mkdir .vscode
  $ touch .vscode/launch.json
  ```

  ```json:.vscode/launch.json
  {
    "version": "0.2.0",
    "configurations": [
      {
        "name": "Gatsby develop",
        "type": "node",
        "request": "launch",
        "protocol": "inspector",
        "program": "${workspaceRoot}/node_modules/gatsby/dist/bin/gatsby",
        "args": ["develop"],
        "stopOnEntry": false,
        "runtimeArgs": ["--nolazy"],
        "sourceMaps": false
      },
      {
        "name": "Gatsby build",
        "type": "node",
        "request": "launch",
        "protocol": "inspector",
        "program": "${workspaceRoot}/node_modules/gatsby/dist/bin/gatsby",
        "args": ["build"],
        "stopOnEntry": false,
        "runtimeArgs": ["--nolazy"],
        "sourceMaps": false
      },
      {
        "name": "Launch Chrome",
        "type": "chrome",
        "request": "launch",
        "url": "http://localhost:8000",
        "webRoot": "${workspaceFolder}"
      }
    ]
  }
  ```

### ステップ２ デバッグの開始

- VSCode 上で F5 キーを押すと、デバッグが開始されます。

- なお、launch.json に複数の構成を定義している場合は、デバッグ画面で左上部のドロップダウンリストから Launch Chrome を選択してからデバッグを開始してください。

- その後、GoogleChrome が自動的に起動します。ここで起動したブラウザがデバッグ対象となり、Chrome 拡張機能の React DevTools が導入されていれば、ここで実際にアプリを操作しながら、VSCode 上でブレークポイントを設定したり、ウォッチ式で変数の監視ができるようになります。

## 参考文献

- [Qiita ｜ VSCode で gatsby のデバッグをする](https://qiita.com/3S_Laboo/items/8a963cd87d917a8bd3c9)
