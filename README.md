## 最新イメージ取得

docker pull php

## バージョン指定

docker pull php:7.4.23-cli

# コンテナ起動

docker run -it --rm -d --name php-app php
docker run -it --rm -d --name php-app php:7.4.23-cli

# コンテナ停止

docker stop php-app

# bash

docker exec -it php /bin/bash

# 滅びの呪文

## docker-compose 管理下のものを全て削除する

docker-compose down --rmi all --volumes --remove-orphans

## ボリュームのみ削除

docker-compose down --volumes
