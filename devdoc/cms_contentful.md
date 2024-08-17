# Contentful

ここでは、GatsbyJS へ Contentful を連携する手順を記します。

## 環境変数の設定

環境変数をファイルから利用するためのライブラリ dotenv をインストールします。

```sh
$ npm install --save dotenv
```

プロジェクト直下に.env.development ファイルを用意し、先程確認した値を設定します。
このファイルに設定することで、開発環境下で環境変数として利用することができます。

```sh:.env.development
GATSBY_CONTENTFUL_SPACE_ID=[スペースID]
GATSBY_CONTENTFUL_API_KEY=[APIキー]
```

## プラグインの導入

gatsby-source-contentful を導入することで Gatsby と Contentful の連携が行なえます。

```sh
$ npm install --save gatsby-source-contentful
```

新しい画像プラグインも導入していきます。これにより、静的画像用(StaticImage)と動的画像用(GatsbyImage)の画像コンポーネントが使用できるようになります。

```sh
$ npm install gatsby-plugin-image gatsby-plugin-sharp gatsby-source-filesystem gatsby-transformer-sharp
```

Contentful から取得したデータの中の body は markdown 形式でデータが保存されており、表示する際には HTML に変換する必要があります。Markdown のデータを GraphQL 上で HTML に変換できる Gatsby のプラグインをインストール。

```sh
マークダウンファイルのHTML変換するGraphQL用プラグイン導入
$ npm install gatsby-transformer-remark
```

gatsby-config.js に利用する環境変数ファイルとプラグイン情報を書くことができ、以下のように設定します。
.env.development はデフォルトで.gitignore に追加されているため、バージョン管理されずローカルにのみ保存されます。そのため、Github にソースコードをアップロードした際に API のキーが外部に公開されることを防いでいます。

```js:gatsby-config.js
require("dotenv").config({
  path: `.env.${process.env.NODE_ENV}`,
})

module.exports = {
  siteMetadata: {
    title: "Dev Blog",
    description: "Gatsbyで作成したブログサイトです。",
    author: "Engineer X"
  },
  plugins: [
    `gatsby-plugin-image`,
    `gatsby-plugin-sharp`,
    `gatsby-transformer-sharp`, // Needed for dynamic images
    {
      resolve: `gatsby-source-contentful`,
      options: {
        spaceId: process.env.GATSBY_CONTENTFUL_SPACE_ID,
        accessToken: process.env.GATSBY_CONTENTFUL_API_KEY
      }
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
  ],
}
```

## 参考文献

- [Zenn ｜ GatsbyJS へ Contentful を連携](https://zenn.dev/tomokiya/books/4b13342f6d878b93e06c/viewer/3e632620995d48d0c84d)
