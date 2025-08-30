FROM php:8.3-apache

ENV TZ=Asia/Jakarta

RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime \
    && ln -s /usr/include/x86_64-linux-gnu/gmp.h /usr/local/include/ \
    && echo $TZ > /etc/timezone \
    && apt-get update \
    && apt-get -y --no-install-recommends install \
        apt-utils curl zip unzip \
        procps git nano wget sqlite3 \
        zlib1g-dev libgpgme11 libgpgme11-dev \
        libfreetype6-dev libjpeg62-turbo-dev libmcrypt-dev libreadline-dev \
        libgmp-dev libmhash-dev libpng-dev libxml2-dev libssl-dev libzip-dev libpq-dev \
        libicu-dev \
        re2c apache2-utils openssl autoconf pkg-config \
    && docker-php-ext-install pdo_mysql opcache zip \
    && docker-php-ext-configure gd --with-jpeg \
    && docker-php-ext-install -j$(nproc) gd \
    && docker-php-ext-install soap mysqli intl bcmath pcntl \
    && docker-php-ext-configure gmp \
    && docker-php-ext-install gmp \
    && docker-php-ext-configure pgsql --with-pgsql=/usr/local/pgsql \
    && docker-php-ext-install pdo_pgsql pgsql \
    && apt-get clean && rm -rf /var/lib/apt/lists/*
