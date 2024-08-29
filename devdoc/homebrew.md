# 環境構築（Homebrew）
[⌘] + [スペース] のSpotlightにて「ターミナル」を検索して「ターミナル.app」を起動します。

## Shell
現在のMacの標準である「zsh」となっているか確認し、「zsh」にしていきましょう。

1. Macのshellが、bash(ﾊﾞｯｼｭ)となっているかzsh(ｻﾞｯｼｭ)となっているか確認する
```
echo $SHELL
```

2. bashに切替する場合はコマンド実行
```
chsh -s /bin/bash
```

3. zshに切替する場合はコマンド実行
```
chsh -s /bin/zsh
```

## Homebrew
Homebrewはコマンドラインでアプリのインストールができるパッケージマネージャー

1. Homebrew存在確認
```
brew -v
```

2. 公式サイトから最新のインストールコマンドを入手
【Homebrew】https://brew.sh/ja/

3. Homebrewインストール

    ```
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```
    * 「Password:」と表示されたら、管理者ユーザのパスワードを入力してEnter
    * 「Press RETURN」と表示されたら、Enterを押して続行
    * 「Downloading Command Line Tools for Xcode」と表示されたらXcodeイントール完了まで待機

4. 残るアップデートがないか確認
```
brew update
```
    * 「Already up-to-date.」と表示されれば残るアップデートはありません

5. Homebrewバージョン確認
```
brew -v
```
    * Homebrew 4.1.5

6. 依存パッケージ存在確認（CLT, Xcode）
```
brew --config
```
    * CLT: 13.3.0
    * Xcode: 13.3.0

## nodebrew
nodebrewは異なるNode.jsを切り替えて開発することができるパッケージマネージャー

1. nodebrew存在確認
```
nodebrew -v
```

2. Homebrewを用いて、nodebrewをインストール
```
brew install nodebrew
```

3. Shellがzshの場合は、zshのプロファイルに環境パスを通す。
```
echo 'export PATH=$HOME/.nodebrew/current/bin:$PATH' >> ~/.zprofile
```

4. nodebrewバージョン確認
```
nodebrew -v
```
    * nodebrew 1.2.0

## Node.js
nodebrewを用いて複数バージョンのNode.jsをインストール

1. インストール可能なNode.jsのバージョンを確認
```
nodebrew ls-remote
```

2. 何かエラーが起こる時にはセットアップ
```
nodebrew setup
```

3. nodebrewを使って複数バージョンのNode.jsをインストール

    ```
nodebrew install-binary v16.14.2  # Node 16 の当時ステーブル版
nodebrew install-binary stable    # 安定版の中で最新バージョンのnode.jsをインストール
```

4. Node.js 使用バージョン指定
    * Udemyでは、React教材のNode.jsバージョンと合わせたNode.js 使用バージョンを指定して取り組みましょう。

    ```
nodebrew ls                       # インストールされているバージョン一覧を表示
nodebrew use v20.5.1              # 使用するバージョンを指定｜任意のバージョンを使用バージョンとしてください
```

5. Node.js バージョン確認
```
node -v
```
    * v20.5.1

6. npm バージョン確認
```
npm -v
```

## プロジェクト依存
1. はじめに
    * Node.js団体が標準として提供している npm にてパッケージ管理が基本になります。他を指定されない限り npm 推奨です。
    * 標準の npm ではビルドが遅いということもあり、プロジェクトにより yarn や vita も使われる場合があります。
    * ただし、プロジェクトで指定がない限り、 npm を用いておくことが想定外エラーに出くわさない推奨手順でございます。

## yarn
Udemyの教材でyarnを用いている場合は合わせてyarnも導入しておきます。

1. yarn 存在確認
```
yarn -v
```

2. npmを用いてyarnをインストール
```
npm install -g yarn
```

3. yarn バージョン確認
```
yarn -v
```

## 参考文献
YouTube｜2021年版｜Node.js入門！使い方〜インストールまで｜https://www.youtube.com/watch?v=wtb0V6a4FXQ