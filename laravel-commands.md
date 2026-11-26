# Laravelのコマンド

## 環境構築

### 事前準備

- Docker Desktopをインストールしておく
- Laravel Sailを使用する際はDocker Desktopを起動する

[Docker Desktop公式サイト](https://www.docker.com/products/docker-desktop/)

#### 1-1. Homebrewのインストール

[Homebrewの公式サイト](https://brew.sh/ja/)

公式サイトからインストールコマンドをコピーしてターミナルで実行する

### Mac

#### 1-2. Homebrewのバージョン確認

```bash
brew --version
# または
brew -v
```

#### 2-1. PHPのインストール

```bash
brew install php
```

#### 2-2. PHPのバージョン確認

```bash
php --version
# または
php -v
```

#### 3-1. Composerのインストール

```bash
brew install composer
```

#### 3-2. Composerのバージョン確認

```bash
composer --version
# または
composer -V
```

#### 4-1. Laravelインストーラーのインストール

```bash
composer global require laravel/installer
```

- `global` : 特定のプロジェクトに依存せず、現在のユーザーが使えるようにする
- `require` : パッケージを追加する

#### 4-2. Laravelインストーラーのバージョン確認

```bash
laravel --version
# または
laravel -V
```

#### 5-1. Laravelでプロジェクトを作成

```bash
laravel new プロジェクト名
```

- 5-1と5-2はどちらか一方を実行する
- 最新バージョンで作成する場合はこちら
- 課題動画での選択内容
  - スターターキット：None
  - データベース：PostgreSQL
  - マイグレーション：Yes
  - npm installとnpm run build：Yes

#### 5-2. Laravelのバージョンを指定(12)してプロジェクトを作成

```bash
composer create-project laravel/laravel プロジェクト名 "12.*"
```

- Laravelインストーラーを使用せず、Composerから作成する
- バージョンを指定する場合はこちら
- Laravelインストーラーのような対話形式の選択画面は表示されない
- npmパッケージのインストールとビルドは手動で行う
- PostgreSQLの設定はLaravel Sailの環境設定時に行う

#### 5-3. Laravel本体のバージョン確認

```bash
php artisan --version
# または
php artisan -V
```

- Laravelプロジェクトの直下ディレクトリで実行する
- Laravelインストーラーではなく、Laravel本体のバージョンを確認する

#### 6-1. Node.jsのバージョン確認

```bash
node --version
# または
node -v
```

- Node.js : JavaScriptをブラウザの外で実行するための環境

Node.jsがインストールされていない場合

```bash
brew install node
```

- Node.jsとnpmをインストールする

#### 6-2. npmのバージョン確認

```bash
npm --version
# または
npm -v
```

- npm : JavaScriptのパッケージを管理するツール

#### 7-1. npmパッケージのインストール

```bash
npm install
# または
npm i
```

- Laravelプロジェクトの直下ディレクトリで実行する。**プロジェクトごとにインストール必要**
- `package.json` に記載されたパッケージをインストールする
- `node_modules` フォルダと`package-lock.json` が生成される
- **npm本体ではない。npmを使ってプロジェクトに必要なパッケージをインストールする(`Vite`、`Tailwind CSS`など)**

#### 7-2. フロントエンドのビルド

```bash
npm run build
```
- CSSやJavaScriptをブラウザで実行できる形式に変換・最適化する

#### 8-1. Laravel Sailのインストール

```bash
composer require laravel/sail --dev
```
- Laravelプロジェクトの直下ディレクトリで実行する
- `require` : パッケージを追加する
- `--dev` : 開発環境用として追加する
- Laravel Sail : Dockerを使用したLaravelの開発環境を構築・操作するためのツール

#### 8-2. Laravel Sailのバージョン確認

```bash
composer show laravel/sail
```

- Laravel Sailのバージョンやインストール先などを確認する

#### 8-3. Laravel Sailの環境設定

```bash
php artisan sail:install
```

- Laravelプロジェクトの直下ディレクトリで実行する
- `artisan` : Laravelをコマンドで操作するためのCLIツール（コマンドラインインターフェース）
- `sail:install` : Laravel Sailを使用するためのDocker開発環境を設定するArtisanコマンド
- データベースの選択
  - Spaceキー：選択・選択解除
  - Enterキー：確定
  - 課題動画ではPostgreSQL（pgsql）のみ選択する
- `compose.yaml` が生成される
- `.env` のデータベース接続設定が変更される（先程の選択したデータベースに変更）

#### 8-4. Laravel Sailの起動

```bash
./vendor/bin/sail up
# または
./vendor/bin/sail up -d
```

- **Docker Desktopが起動している必要がある**
- Laravelプロジェクト直下で実行する
- `./vendor/bin/sail` : Laravel Sailの実行ファイル
- `up` : Dockerコンテナを起動する
- `-d` : detached（デタッチド）。バックグラウンドで起動する
- バックグラウンドで起動すると、同じターミナルで引き続きコマンドを実行できる
- 初回起動時に`sessions` テーブルが存在しないエラーが発生する場合がある
- その場合は8-5のマイグレーションを実行する

#### 8-5. マイグレーションの実行

```bash
./vendor/bin/sail artisan migrate
```

- Laravelプロジェクトの直下ディレクトリで実行する
- **Docker DesktopとLaravel Sailが起動している必要がある**
- `migrate` : マイグレーションを実行する
- マイグレーションファイルに基づいて、データベースのテーブルを作成・変更する
- Laravel Sail経由でDockerコンテナのArtisanコマンドを実行する
- 8-4で`-d` を付けてバックグラウンドでLaravel Sailを起動していなければ、もう一つターミナルを起動して、そこで実行する

#### 8-6. ブラウザでの動作確認

[http://localhost](http://localhost)にアクセスする。

- Laravelの初期画面が表示されれば環境構築は成功（やったね！）
- `sessions` テーブルが存在しないエラーが出た場合は、マイグレーションの実行状況を確認する

#### 8-7. Laravel Sailの停止

```bash
./vendor/bin/sail down
```

- 通常起動時（`-d` なし）は `Control + C` で停止できる（コンテナの削除ではない）
- `down` Dockerコンテナを停止・削除し、ネットワークも削除する
- バックグラウンド起動時（`-d` あり）も停止できる
- データベースのデータは通常、Dockerボリュームに保持される
- **注意：`down -v` を実行するとDockerボリュームも削除されるため、データベースのデータが失われる**

### 比較

| 役割 | PHP | JavaScript |
|---|---|---|
| パッケージ管理ツール | `Composer` | `npm` |
| インストールコマンド | `composer install` | `npm install` |
| インストールするパッケージの指定 | `composer.json` | `package.json` |
| パッケージの保存先 | `vendor` | `node_modules` |
| バージョンの記録 | `composer.lock` | `package-lock.json` |