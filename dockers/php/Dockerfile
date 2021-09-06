# PHPイメージ
FROM php:7.4.23-fpm-buster

# 関連パッケージをインストール
RUN apt-get update && \
    apt-get install -y vim && \
    apt-get install -y unzip && \
    apt-get install -y libicu-dev && \
    docker-php-ext-install intl && \
    docker-php-ext-install pdo_mysql

