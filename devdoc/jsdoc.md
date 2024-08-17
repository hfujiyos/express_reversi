# JSDoc

- JSDoc コメントとは関数や変数の宣言の直前に/\*_ ◯◯ _/を書く記法。
- JSDoc コメントはコード入力時にツールチップでコードヒントが表示されます。
- プログラムのコードヒントの表示や補完入力の手助けとなっています。

## JSDoc（JavaScript）

- JSDoc コメントには{string}や{number}などで型を記載できます。
- JavaScript の場合は、型を追跡できる手がかりは JSDoc コメントしかないので記載することが望ましいです。

  ```js
  /**
   * Helloを付与する関数です。
   * @param {string} message メッセージ
   * @return {string} 加工された文字列
   */
  function sayHello(message) {
    return `Hello ${message}`
  }
  ```

## JSDoc（TypeScript）

- TypeScript では型注釈（アノテーション）によって、言語文法として型情報を記載できます。
- そのため、わざわざ JSDoc コメントに型情報を記述する必要はありません。

  ```ts
  /**
   * Helloを付与する関数です。
   * @param message メッセージ
   * @return 加工された文字列
   */
  function sayHello(message: string): string {
    return `Hello ${message}`
  }
  ```
