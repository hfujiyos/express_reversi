# GitHubFlow

## 1. 初期ブランチ構築（スクラムマスター）

- Git初回設定

  ``sh
  git config --global init.defaultBranch main           # デフォルトブランチ名を main に変更
  git config --global user.name "会社用のユーザーネーム"    # デフォルトユーザー名を指定
  git config --global user.email "会社用のメールアドレス"   # デフォルトメールアドレスを指定
  ```

-- 開発ディレクトリを作成

  ```sh
  mkdir /Development/springboot/springboot_todoapi
  cd /Development/springboot/springboot_todoapi
  ```

- ローカルリポジトリを設定

  ```sh
  git init
  git branch -m master main
  ```

- リモートリポジトリに main ブランチ作成
  * GitHubにログインします
  * 右上の「New repository」ボタンをクリックします
  * リポジトリを作成します
    * Repository name: プロジェクト名（例: springboot_todoapi）
    * Description: オプションでプロジェクトの説明を入力します
    * Visibility: 「Public」または「Private」を選択します
    * 「Create repository」ボタンをクリックしてリポジトリを作成します
  * 必要に応じて追加設定
    * プルリクエストがマージされた後、ヘッドブランチを自動的に削除
    ☑︎Automatically delete head branches

- リモートリポジトリを設定

    ```sh
    git remote add origin git@github.com:hfujiyos/springboot_todoapi.git      # SSH接続の場合
    ```

- 初回リモートプッシュ

  ```sh
  git add .                           # ステージング
  git commit -m "initial commit"      # コミット
  git push -u origin main             # プッシュ
  ```

## 2. イシュー定義（レビュア）

- イシュー作成と開発者アサイン

  ```
  Add login mock
  Fix login logic
  ```

## 3. チケット駆動開発（開発者）

- 開発ディレクトリを作成

  ```sh
  mkdir Development/Springboot_todoapi
  cd Development/Springboot_todoapi
  ```

- リモートリポジトリをクローン

  ```sh
  git clone git@github.com:hfujiyos/springboot_todoapi.git
  cd springboot_todoapi
  code .
  ```

- 最新ソースをプル

  ```sh
  git checkout main     # mainブランチに切替
  git pull              # リモートリポジトリから最新ソースをプル
  ```

- ローカルリポジトリにfeatureブランチ作成

  ```sh
  git checkout -b feature/fixLoginLogic
  ```

- 最新HEADをリモートプッシュ

  ```sh
  git add .                           # ステージング
  git commit -m "Fix login logic"     # コミット
  git push origin HEAD                # プッシュ
  ```

- プルリクエスト（リモートfeatureをリモートmainへのマージ依頼）

  * マージする際にイシューもクローズする際にはコメント付与
  ```
  close #9
  ```

## 4. コードレビュー（レビュア）

- レビュアにて、コードレビュー / 承認


## 5. 後工程（開発者）

- レビュアの承認を受けたら、開発者にてmainブランチへマージ

- ローカルmainにリモートmainの最新ソースをプル

  ```sh
  git checkout main     # mainブランチに切替
  git pull              # リモートリポジトリから最新ソースをプル
  ```

- ローカルfeatureを削除

  ```sh
  # 現在のブランチがmainであるか確認
  git branch
    feature/funcE
  * main

  # ローカルリポジトリの不要ブランチを削除
  git branch -D feature/funcE

  # 不要ブランチが削除されていることを確認
  git branch
  * main
  ```

## 【番外編】Git 作業にミスしたとき

### 直前にコミットしたメッセージを変更する

- 直前コミットのメッセージのみを変更する

  ```sh
  git add -A
  git commit -m "htmlを修正"
  # あっ　今のコミット内容、cssの修正だった！書き直したい…！
  git commit --amend -m "cssを修正"
  # これで直前のコミットが更新されました！
  ```

### コミットの内容を取り消して無かったことにして最初からやり直したい

- 作業ディレクトリ

  - 変更・作成したもの全てリセットされる（直前のコミット状態になる）

- ステージングエリア

  - アンステージされる

  ```sh
  # 直前のコミットの状態に戻る
  git reset --hard HEAD
  ```
