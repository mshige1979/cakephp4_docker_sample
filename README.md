## git clone

    git clone https://github.com/mshige1979/cakephp4_docker_sample.git

## docker build

### dcoker-compose build

    docker-compose build --no-cache

### 起動

    docker-compose up -d

### 終了

    docker-compose down

## cakephp install

### コンテナへ入る

    docker exec -it php /bin/bash

### ディレクトリ移動

    cd /var/www

### インストール

    composer self-update && composer create-project --prefer-dist cakephp/app:4.* html

### 動作確認

    cd /var/www/html
    bin/cake server -H 0.0.0.0 -p 4321

## 参考リンク

    https://book.cakephp.org/4/ja/installation.html
    https://tt-computing.com/docker-cake4-nginx-mysql
    https://qiita.com/ucan-lab/items/a388e214d4e4ed4630b1
