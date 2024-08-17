# Strapi

## Node.js

- nodebrew を用いて複数バージョンの Node.js を管理

  ```sh
  インストール可能なNode.jsのバージョンを確認
  $ nodebrew ls-remote

  何かエラーが起こる時にはセットアップ
  $ nodebrew setup

  nodebrewを使って指定バージョンのNode.jsをインストール
  $ nodebrew install-binary v14.20.0  # Strapiで使用できるNode 10, 11, 12, 13, 14内の最新版
  ```

- Node.js 使用バージョン指定

  ```sh
  インストールされているバージョン一覧を表示
  $ nodebrew ls
  v14.20.0
  v16.14.2

  使用するバージョンを指定
  $ nodebrew use 14.20.0

  Node.js バージョン確認
  $ node -v
  v14.20.0

  npm バージョン確認
  $ npm -v
  6.14.17
  ```

## バックエンド開発環境の構築

- Strapi インストール（プロジェクト名：backend）

  ```sh
  $ npx create-strapi-app@3.4.0 backend

  ? Choose your installation type (Use arrow keys)
  ❯ Quickstart (recommended)
    Custom (manual settings)
  ```

## 開発環境動作確認

- 開発環境動作確認

  ```sh
  $ npm run develop
  ```

  http://localhost:1337
  http://localhost:1337/admin
