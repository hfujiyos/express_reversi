# vscode-js-debug

- React.js の場合は CSR をデバッグします。Next.js の場合は SSR をデバッグします。
- 上記のため、VSCode の launch.json にてデバッガをアタッチするポート番号に注意します。
- 最新のデバッガは `pwa-chrome` ですが、 `chrome` でも問題ありません

## Next.js を VSCode でデバッグする

### ステップ１ Next.js をデバッグモードで起動する

- まずは next を起動する時に NODE_OPTIONS='--inspect'を渡すようにします。
- 具体的には package.json の dev コマンドを以下のように書き換えます。

```json:package.json
"dev": "NODE_OPTIONS='--inspect' next dev"
```

### ステップ２ VS Code のデバッガーを起動する

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
      "type": "node",
      "request": "attach",
      "name": "Launch Program",
      "skipFiles": ["<node_internals>/**"],
      "port": 9229
    }
  ]
}
```

### ステップ３ ブレークポイントを貼って状態を確認する

- ここまでできたら準備完了です。
- `npm run dev` を実行してサーバーを立ち上げます。
- VS Code のデバック画面に行って Launch Program を実行してデバッガをアタッチします。
- 適当なところにブレークポイントを貼理、画面をリロードしたらデバッグできるようになります。

## 参考文献

- [【Next.js】VS Code で Next.js をデバッグするやり方](https://techblog.lclco.com/entry/2020/12/23/000000)
