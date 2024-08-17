# GatsbyJS

## 開発環境の構築

- バージョン確認

  ```sh
  $ node -v
  v16.14.2
  $ npm -v
  8.7.0
  ```

- GatsbyJS グローバルインストール

  ```sh
  $ npm install -g gatsby-cli
  $ gatsby -v
  Gatsby CLI version: 4.18.1
  ```

- GatsbyJS テンプレート（gatsby-starter-hello-world）のインストール

  ```sh
  $ gatsby new gatsbyjs-site https://github.com/gatsbyjs/gatsby-starter-hello-world
  ```

- 開発環境動作確認

  ```sh
  $ cd gatsbyjs-site
  $ gatsby develop
  ```

  http://localhost:8000/

## Contentful を利用する環境変数設定

- 環境変数をファイルから利用するためのライブラリ dotenv をインストール

  ```sh
  $ npm install --save dotenv
  ```

- プロジェクト直下に.env.development ファイルを用意

  ```sh:.env.development
  GATSBY_CONTENTFUL_SPACE_ID=[スペースID]
  GATSBY_CONTENTFUL_API_KEY=[APIキー]
  ```

## 追加ライブラリ導入

- Contentful 連携のライブラリ導入

  ```sh
  Contentful 連携のライブラリ導入
  $ npm install --save gatsby-source-contentful
  ```

  ```sh
  画像プラグインのライブラリ導入
  $ npm install gatsby-plugin-image gatsby-plugin-sharp gatsby-source-filesystem gatsby-transformer-sharp
  ```

- GraphQL 連携のライブラリ導入

  ```sh
  ローカルファイルシステムへのアクセス用プラグイン導入
  $ npm install gatsby-source-filesystem
  ```

  ```sh
  マークダウンファイルのHTML変換するGraphQL用プラグイン導入
  $ npm install gatsby-transformer-remark
  ```

- SEO 連携のライブラリ導入

  ```sh
  headタグを管理するプラグイン導入
  $ npm install --save react-helmet
  ```

- gatsby-config.js に利用する環境変数ファイルとプラグイン情報を記述

  ```js:gatsby-config.js
  require("dotenv").config({
    path: `.env.${process.env.NODE_ENV}`,
  })

  module.exports = {
    siteMetadata: {
      title: "Dev Blog",
      description: "Gatsbyで作成したブログサイトです。",
      author: "Engineer X",
    },
    plugins: [
      `gatsby-plugin-image`,
      `gatsby-plugin-sharp`,
      `gatsby-transformer-sharp`, // Needed for dynamic images
      {
        resolve: `gatsby-source-contentful`,
        options: {
          spaceId: process.env.GATSBY_CONTENTFUL_SPACE_ID,
          accessToken: process.env.GATSBY_CONTENTFUL_API_KEY,
        },
      },
      {
        resolve: `gatsby-transformer-remark`,
        options: {
          commonmark: true,
          footnotes: true,
          pedantic: true,
          gfm: true,
          plugins: [],
        },
      },
      {
        resolve: `gatsby-source-filesystem`,
        options: {
          name: `src`,
          path: `${__dirname}/src/`,
        },
      },
    ],
  }
  ```

## ディレクトリ構成

- Gatsby ディレクトリ構成

  | ディレクトリ      | 説明                                                 |
  | :---------------- | ---------------------------------------------------- |
  | node_modules      | npm を用いてインストールしたパッケージ               |
  | public            | 事前にビルドし作成された HTML が格納される           |
  | src/components    | ページ全体の配置を整えるための Layout コンポーネント |
  | src/pages         | ページを構成するソースコードの置き場所               |
  | src/styles        | スタイルを構成するソースコードの置き場所             |
  | static            | 画像や favicon の置き場所                            |
  | gatsby-browser.js | サイト全体で読み込みするグローバルスタイル           |
  | gatsby-config.js  | サイト meta データやプラグインを設定                 |
  | package.json      | npm で管理するパッケージ情報を記載したファイル       |

## Gatsby CLI

- 新規プロジェクトを作成する

  ```sh
  $ gatsby new <site-name> <starter-url>
  ```

- 開発サーバーの立ち上げ

  ```sh
  $ gatsby develop
  ```

  | オプション | 説明                                                                                   |
  | :--------- | -------------------------------------------------------------------------------------- |
  | -H, --host | host 名を設定できます。デフォルトは localhost になっています。                         |
  | -p, --port | ポートを設定できます。デフォルトは 8000 もしくは 環境変数の env .PORT を読み込みます。 |
  | -o, --open | サーバーが立ち上がった際にブラウザでページを開けます。                                 |

- デプロイ用のコンパイル

  本番にデプロイする前に使うコマンドです。

  ```sh
  $ gatsby build
  ```

  | オプション | 説明                                                           |
  | :--------- | -------------------------------------------------------------- |
  | -H, --host | host 名を設定できます。デフォルトは localhost になっています。 |
  | -p, --port | ポートを設定できます。デフォルトは 9000 になっています。       |
  | -o, --open | サーバーが立ち上がった際にブラウザでページを開けます。         |

- キャッシュを削除する

  開発時に更新内容が反映されない場合に使います。
  内容としては、.cache と public ディレクトリを削除します。

  ```sh
  $ gatsby clean
  ```

## 参考文献

- [Zenn ｜ブログサイトを作りながら学ぶ Gatsby 入門](https://zenn.dev/tomokiya/books/4b13342f6d878b93e06c)
- [REFFECT ｜基礎から始める GatsbyJS 入門](https://reffect.co.jp/react/gatsby-basic-tutorial-for-beginners#Blog_Starter)
- [YouTube ｜マイケル｜ Gatsby 入門](https://bit.ly/3PytG4m)
- [GatsbyJS 公式サイト｜ How to use gatsby-cli](https://www.gatsbyjs.com/docs/reference/gatsby-cli/)
- [GatsbyJS テンプレート｜ gatsby-starter-blog](https://www.gatsbyjs.com/starters/gatsbyjs/gatsby-starter-blog)
