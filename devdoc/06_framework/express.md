# Reversi

## 基本設計（docs）

1. コンテキスト図｜context-diagram.drowio
2. ユースケース図｜use-case.drowio
3. モデル図｜conseptual-model.drowio
4. 機能一覧設計書｜features.md
5. 画面定義設計書｜ui.drowio

## 詳細設計（docs）

1. WEBAPI設計書｜webapi-design-memo.md
2. OpenAPI設計書｜openapi.yaml
3. ER図｜er.drowio

## Mac-VSCodeショートカット
* SwaggerUI表示 ｜shipt + option + P
* ターミナル表示　｜control + shift + ^
* ターミナルクリア｜command + K

## 開発環境セットアップ

1. Node.js バージョン 16.17.1を用意

    ```console
    # Node.js バージョン 16.17.1をインストールして使用
    nodebrew install-binary v16.17.1    # Reversiで使用するNode 16の安定版
    nodebrew ls                         # インストールされているバージョン一覧を表示
    nodebrew use v16.17.1               # 使用するバージョンを指定｜任意のバージョンを使用バージョンとしてください
    ```

2. 開発ディレクトリを用意

    ```console
    # 開発ディレクトリに移動
    cd Development
    mkdir Reversi        // Reversiディレクトリが無ければ作成
    cd Reversi           // Reversiディレクトリに移動
    ```

3. TypeScriptインストール

    ```console
    # npmセットアップ
    npm init
    # TypeScriptインストール
    npm install --save-dev typescript@4.8.3 ts-node@10.9.1
    # TS実行
    npx ts-node hello.ts
    ```

4. Expressインストール

    ```console
    # Expressインストール
    npm install express@4.18.1
    # ExpressのTypeScript化
    npm install --save-dev @types/express@4.17.14
    # TS実行
    npx ts-node src/main.ts              # TS実行
    http://localhost:3000/api/hello      # ブラウザ動作確認
    control + C                          # ts-node停止
    ```

5. nodemonインストール（ホットリロード設定のため）

    ```console
    # nodemonインストール
    npm install --save-dev nodemon@2.0.20
    ```

  * nodemon.json

    ```json
    {
        "watch": ["src"],
        "ext": "ts",
        "exec": "ts-node src/main.ts"
    }
    ```

  * package.json

    ```json
    "scripts": {
        "start": "nodemon",
        "test": "echo \"Error: no test specified\" && exit 1"
    },
    
    ```console
    # nodemon実行
    npm start              # nodemon実行
    http://localhost:3000/api/hello      # ブラウザ動作確認
    control + C                          # nodemon停止
    ```

6. morganインストール（アクセスログ設定のため）

    ```console
    # morganインストール
    npm install morgan@1.10.0                   # morganインストール
    npm install --save-dev @types/morgan@1.9.3  # morganのTypeScript化
    ```

7. express-async-errorsインストール（エラーハンドリングのため）

    ```console
    # express-async-errorsインストール
    npm install express-async-errors@3.1.1
    ```

8. Dockerインストール

  * Dockerダウンロード
    * https://hub.docker.com/editions/community/docker-ce-desktop-mac
    * CPUが M1 Macの場合は「Docker Desktop for Mac with Apple silicon」を選択
    * CPUが Intel Macの場合は「Docker Desktop for Mac with Intel chip」を選択

  * Dockerのインストール
    * インストールが完了すれば、LaunchpadにDockerのマークが現れます。
    * ターミナルから、docker versionとdocker-compose versionを実行してバージョン確認

  * docker-compose.yaml

    ```yaml
    version: '3'
    services:
    mysql:
        image: mysql:8.0.29
        platform: linux/x86_64
        ports:
        - 3306:3306
        environment:
        MYSQL_ROOT_PASSWORD: rootpassword
        MYSQL_DATABASE: reversi
        MYSQL_USER: reversi
        MYSQL_PASSWORD: password
    deploy:
      resources:
        limits:
          memory: 2g
    ```
  
  * Docker初回起動

    ```console
    # Docker Hub ログイン
    docker login
    # Docker起動
    docker-compose up -d
    # Docker起動確認
    docker-compose ps
    # Dockerログ確認
    docker-compose logs -f
    ```

  * Docker再起動

    ```console
    # Docker停止
    docker-compose down
    # Docker起動確認
    docker-compose ps
    # Docker起動
    docker-compose up -d
    ```

8. MySQL接続

  * bin/connect_mysql.sh

    ```sh
    #!/bin/bash
    docker-compose exec mysql mysql --user=reversi --password=password reversi
    ```

    ```console
    chmod +x ./bin/connect_mysql.sh     # 実行権限付与
    ./bin/connect_mysql.sh              # MySQL接続シェル実行
    ```

    ```sql
    show databases;
    exit
    ```

9. CREATE TABLE実行

  * bin/load_ddl.sh

    ```sh
    #!/bin/bash
    cat mysql/init.sql | docker-compose exec -T mysql mysql --user=root --password=rootpassword
    ```

    ```console
    chmod +x ./bin/load_ddl.sh     # 実行権限付与
    ./bin/load_ddl.sh              # CREATE TABLEシェル実行
    ./bin/connect_mysql.sh              # MySQL接続シェル実行
    ```

    ```sql
    show tables;
    exit
    ```

10. MySQLインストール

    ```console
    # MySQLインストール
    npm install mysql2@2.3.3
    ```
