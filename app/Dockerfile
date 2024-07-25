# ベースイメージとしてUbuntuを使用
FROM ubuntu:20.04

# 環境変数の設定
ENV DEBIAN_FRONTEND=noninteractive

# 必要なパッケージをインストール
RUN apt-get update && \
    apt-get install -y software-properties-common && \
    add-apt-repository ppa:ondrej/php && \
    apt-get update && \
    apt-get install -y \
    php8.0 \
    php8.0-cli \
    php8.0-fpm \
    php8.0-mysql \
    php8.0-pgsql \
    php8.0-sqlite3 \
    php8.0-xml \
    php8.0-mbstring \
    php8.0-curl \
    php8.0-zip \
    php8.0-bcmath \
    php8.0-intl \
    php8.0-gd \
    php8.0-opcache \
    php8.0-redis \
    curl \
    git \
    unzip \
    nano && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

# Composerのインストール
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

# 作業ディレクトリを設定
WORKDIR /var/www

# 新しいLaravelプロジェクトを作成
RUN composer create-project --prefer-dist laravel/laravel laravel

# Laravelプロジェクトのディレクトリに移動
WORKDIR /var/www/laravel

# # PHP-FPMの設定をTCPポートでリッスンするように変更（必要に応じて）
# RUN sed -i 's/listen = \/run\/php\/php*.sock/listen = 9000/' /etc/php/*/fpm/pool.d/www.conf

# パーミッションを設定
# RUN chown -R www-data:www-data /var/www && \
#     chmod -R 755 /var/www/storage

# ポートを開放
EXPOSE 9000

# PHP-FPMを起動
CMD ["php-fpm8.0", "-F"]
