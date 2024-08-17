# Apollo Client

## 開発環境の構築

- Apollo インストール

  ```sh
  $ npm i @apollo/react-hooks@3.1.5 @apollo/react-ssr@3.1.5 apollo-boost@0.4.7 apollo-link-http@1.5.17 graphql@15.0.0 next-apollo@3.1.10 --save --legacy-peer-deps
  ```

- Apollo セットアップ

  ```sh
  $ mkdir lib
  $ touch lib/apollo.js
  ```

  ```js:lib/apollo.js
  import { HttpLink } from "apollo-link-http"
  import { withData } from "next-apollo"
  const API_URL = process.env.NEXT_PUBLIC_API_URL || "http://localhost:1337"
  const config = {
    link: new HttpLink({
      uri: `${API_URL}/graphql`,
    }),
  }
  export default withData(config)
  ```

  ```js:pages/_app.js
  import withData from "../lib/apollo"
  class MyApp extends App {
    ･･･
  export default withData(MyApp)
  ```
