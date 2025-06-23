# 使用技術

![Laravel](https://img.shields.io/badge/Laravel-11-brightgreen.svg)
![PHP](https://img.shields.io/badge/PHP-8.3-blue.svg)
![MariaDB](https://img.shields.io/badge/MySQL-8.0.33-blue.svg)
![nginx](https://img.shields.io/badge/nginx-1.27-blue.svg)
![Docker](https://img.shields.io/badge/Docker-26.1.4-blue.svg)
![docker-compose](https://img.shields.io/badge/docker--compose-2.27.1-blue.svg)

# Laravel プロジェクトの作成方法

1. **clone する**  
   プロジェクトのコピーを自分のコンピュータにダウンロードします。

   ```
   git clone git@github.com:arlo-engineer/php83-nginx-mysql.git <ディレクトリ名>
   ```

2. **docker compose で立ち上げる**  
   ダウンロードしたプロジェクトを使って、必要なプログラム（コンテナと呼ばれる）を自動的に起動します。

   ```
   cd <ディレクトリ名>
   docker compose up -d
   ```

3. **php コンテナに入る**  
   起動したプログラムの中の一つ、PHP を使う部分にアクセスします。

   ```
   docker exec -it myapp-php bash
   ```

4. **サブディレクトリに laravel をインストールする**  
   PHP を使って、Laravel をインストールします。
   ```
   composer create-project "laravel/laravel=11.*" myapp --prefer-dist
   ```
   プロジェクトフォルダの中身を移動し、一時ディレクトリを削除
   ```
   mv myapp/* ./
   mv myapp/.* ./
   rm -r myapp
   ```
5. **実行テストする**
   ブラウザで http://localhost にアクセスし、Laravel の welcome ページが表示されることを確認する。

# DB との接続方法

1. Laravel プロジェクト内の.env ファイルを以下のように変更する(変更する値は Laravel プロジェクト外の.env ファイルを参照する)
   ```:.env
   DB_CONNECTION=mysql
   DB_HOST=db # docker-compose.ymlのmysqlのコンテナ名
   DB_PORT=3306
   DB_DATABASE=development
   DB_ROOT_PASSWORD=root
   DB_USERNAME=mysql
   DB_PASSWORD=mysql
   ```
2. 以下を実行し、DB との接続をする
   ```
   php artisan migrate
   ```

# 初期設定

## タイムゾーンと言語

.env ファイルを以下の通り書き換える

```:.env
APP_TIMEZONE=Asia/Tokyo
APP_LOCALE=ja
```

## デバッグバーのインストール

```
composer require barryvdh/laravel-debugbar
```

## 言語ファイル

```
php artisan lang:publish
composer require askdkc/breezejp --dev
php artisan breezejp
```

# リポジトリを変更して push する方法

以下記事を参考にすることで、GitHub リポジトリを変更して push することができる

[GitHub からクローンしたリポジトリを別リポジトリにプッシュしたい](https://k-koh.hatenablog.com/entry/2020/10/09/154644)

※⚠️ リポジトリを変更して push する際は、.env ファイルを Git 管理から除外すること

```
git rm --cached .env
```

# 参考文献

- [Laravel10 の開発環境を docker で実現する方法](https://qiita.com/hitotch/items/869070c3a9f474a358ea)
- [【最新保存版】Laravel 入門基礎マスター講座【初心者もゼロから学習】](https://youtu.be/SXjrlVs5Tnk?si=Dmr5qMVMMF33_ejB)

# 現在の Git 履歴を完全に削除

rm -rf .git

# 新しい Git リポジトリとして初期化

git init

# 現在のファイルをステージング

git add .

# 初回コミット

git commit -m "Initial commit"
