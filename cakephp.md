# cakephp 環境構築メモ

## version:

    php7系
    cakephp4系
    MySQL

## 仕組み

    nginx: リバースプロキシ用
    cakephp: php-fpmでポート9000で起動
    MySQL: 3306
            データはボリューム化して永続化はするが、共有ディレクトリ化はせず、
            dockerホストでの管理下とする

## docker イメージ

    nginx: 既存のものをそのまま利用
    php: php-fpmが内包しているものを利用、存在しない場合は作成
    MySQL: 既存のものを利用

## 方法

### Composer インストール

    php-fpm が入ったコンテナを利用する
    基本、アプリサーバとするため、mysql などの接続も考慮

### Cakephp プロジェクトを作成

    → ビルドでプロジェクトを作成するのではなく、すでに準備冴えているプロジェクトを利用する
     →　プロジェクト作成自体はコンテナに直接入って作成する流れにする
     → ドキュメントルート自体のディレクトリはボリュームで共有ディレクトリを利用し、作成済みの場合はそのままnginxから起動することができる
    → DB は別定義しているが接続はできるかと…

### nginx 設定

    php-fpm、db コンテナが起動した際に起動する仕組み
    ポートは一応、80, 443

### DB 設定

    ルート用ユーザー、ルート用パスワード、接続用ユーザー、接続用パスワード、データベース名を利用する
    ポートは 3306
    データは docker ホストのボリュームを利用

## 参考リンク

    https://book.cakephp.org/4/ja/installation.html
    https://tt-computing.com/docker-cake4-nginx-mysql
    https://qiita.com/ucan-lab/items/a388e214d4e4ed4630b1

## cakephp install

### composer

    php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"
    php -r "if (hash_file('sha384', 'composer-setup.php') === '756890a4488ce9024fc62c56153228907f1545c228516cbf63f885e036d37e9a59d27d63f46af1d4d07ee0f76181c7d3') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;"
    php composer-setup.php
    php -r "unlink('composer-setup.php');"
    mv composer.phar /usr/local/bin/composer
    ↓
    COPY --from=composer /usr/bin/composer /usr/bin/composer

### cakephp

    cd /var/www
    composer self-update && composer create-project --prefer-dist cakephp/app:4.* html
    bin/cake server -H 0.0.0.0 -p 4321

--no-cache
