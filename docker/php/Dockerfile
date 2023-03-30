FROM php:8.1.2-fpm

RUN apt-get update && apt-get install -y  \
    curl \
    nano \
    libonig-dev \
    libxml2-dev \
    libzip-dev \
    unzip \
    git \
    zip \
    libwebp-dev \
    libjpeg62-turbo-dev \
    libpng-dev \
    libxpm-dev \
    libfreetype6-dev \
    libmcrypt-dev \
    libjpeg-dev \
    libcurl4-openssl-dev \
    pkg-config \
    libssl-dev \
    openssl \
    zlib1g-dev \
    libicu-dev \
    g++ \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

RUN docker-php-ext-install pdo_mysql mbstring exif pcntl bcmath zip  gd opcache intl \
    && docker-php-ext-configure gd --with-freetype --with-jpeg \
    && docker-php-ext-install -j "$(nproc)" gd \
    && pecl install redis \
    && docker-php-ext-enable redis

RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

RUN curl -sL https://deb.nodesource.com/setup_14.x | bash -
RUN apt-get install -y nodejs

COPY ./docker/php/php.ini /usr/local/etc/php/

WORKDIR /var/www/html

CMD ["php-fpm"]

EXPOSE 8000 8001 9000

