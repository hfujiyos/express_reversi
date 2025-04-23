# GitHubFlow

## 1. 初期ブランチ構築（スクラムマスター）

- Git 初回設定

  ```sh
  git config --global init.defaultBranch main   # ﾃﾞﾌｫﾙﾄﾌﾞﾗﾝﾁ名をmainに変更
  git config --global user.name "会社用ﾕｰｻﾞｰﾈｰﾑ"   # ﾃﾞﾌｫﾙﾄﾕｰｻﾞｰ名を指定
  git config --global user.email "会社用ﾒｰﾙｱﾄﾞﾚｽ"  # ﾃﾞﾌｫﾙﾄﾒｰﾙｱﾄﾞﾚｽを指定
  ```

-- 開発ディレクトリを作成

```sh
mkdir ~/development/nodejs/express_reversi
cd ~/development/nodejs/express_reversi
```

- ローカルリポジトリを設定

  ```sh
  git init                    # Git初回設定
  git branch -m master main   # ﾌﾞﾗﾝﾁ名をmasterからmainに変更
  ```

- リモートリポジトリに main ブランチ作成

  - GitHub にログインします
  - 右上の「New repository」ボタンをクリックします
  - リポジトリを作成します
    - Repository name: プロジェクト名（例: springboot_todoapi）
    - Description: オプションでプロジェクトの説明を入力します
    - Visibility: 「Public」または「Private」を選択します
    - 「Create repository」ボタンをクリックしてリポジトリを作成します
  - 必要に応じて追加設定
    - プルリクエストがマージされた後、ヘッドブランチを自動的に削除
      ☑︎Automatically delete head branches

- リモートリポジトリを新規設定

  ```sh
  git remote add origin git@github-hfid:hfujiyos/express_reversi.git  # SSH接続の場合
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

- Node.js バージョン確認

  ```sh
  node -v               # nodeﾊﾞｰｼﾞｮﾝ確認
  nodebrew ls           # ｲﾝｽﾄｰﾙされているnodeﾊﾞｰｼﾞｮﾝ一覧を表示
  nodebrew use v20.5.1  # 使用するnodeﾊﾞｰｼﾞｮﾝを設定
  ```

- 開発ディレクトリを作成

  ```sh
  mkdir development/nodejs/express_reversi
  cd development/nodejs/express_reversi
  ```

- リモートリポジトリをクローン

  ```sh
  git clone git@github-hfid:hfujiyos/express_reversi.git  # クローン（SSH接続）
  cd ~/development/nodejs/express_reversi                 # ディレクトリ移動
  code .                                                  # VSCode起動
  ```

- リモートリポジトリの既存修正

  ```sh
  cd ~/development/nodejs/express_reversi
  git remote set-url origin git@github-hfid:hfujiyos/express_reversi.git
  ```

- 最新ソースをプル

  ```sh
  git checkout main     # mainブランチに切替
  git pull              # リモートリポジトリから最新ソースをプル
  ```

- ローカルリポジトリに feature ブランチ作成

  ```sh
  git checkout -b feature/fixLoginLogic
  ```

- 最新 HEAD をリモートプッシュ

  ```sh
  git add .                           # ステージング
  git commit -m "Fix login logic"     # コミット
  git push origin HEAD                # プッシュ
  ```

- プルリクエスト（リモート feature をリモート main へのマージ依頼）

  - マージする際にイシューもクローズする際にはコメント付与

  ```
  close #9
  ```

## 4. コードレビュー（レビュア）

- レビュアにて、コードレビュー / 承認

## 5. 後工程（開発者）

- レビュアの承認を受けたら、開発者にて main ブランチへマージ

- ローカル main にリモート main の最新ソースをプル

  ```sh
  git checkout main     # mainブランチに切替
  git pull              # リモートリポジトリから最新ソースをプル
  ```

- ローカル feature を削除

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
  git commit -m "htmlを修正"          # 誤ったコメントでコミットしてしまった
  git commit --amend -m "cssを修正"   # 直前コミットのコメントを更新
  ```

### コミットの内容を取り消して無かったことにして最初からやり直したい

- 作業ディレクトリ

  - 変更・作成したもの全てリセットされる（直前のコミット状態になる）

- ステージングエリア

  - アンステージされる

  ```sh
  git reset --hard HEAD   # 直前のコミットの状態に戻る
  ```
