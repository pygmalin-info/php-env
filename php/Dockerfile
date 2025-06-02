# Composerのベースイメージ
FROM composer as composer

# PHPのベースイメージ（FPMでNginxと連携）
FROM php:8.3-fpm

# Composer をインストール
COPY --from=composer /usr/bin/composer /usr/bin/composer

# 必要なシステムパッケージをインストール
RUN apt-get update \
    && DEBIAN_FRONTEND=noninteractive apt-get install -y --no-install-recommends \
    unzip \
    libpq-dev \
    && rm -rf /var/lib/apt/lists/*

# PHP拡張をインストール
RUN docker-php-ext-install \
    pgsql \
    pdo_pgsql

RUN useradd -ms /bin/bash phper

# php.iniをコピー
COPY ./php.ini /usr/local/etc/php/php.ini

WORKDIR /app

# アプリケーションのファイルをコピー
COPY . .

USER phper
