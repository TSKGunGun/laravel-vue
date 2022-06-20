FROM php:7.4.1-fpm

#COPY php.ini
COPY ./docker/php/php.ini /usr/local/etc/php/php.ini

#Composer install
COPY --from=composer:2.0 /usr/bin/composer /usr/bin/composer

# install Node.js
COPY --from=node:16.15 /usr/local/bin /usr/local/bin
COPY --from=node:16.15 /usr/local/lib /usr/local/lib

RUN apt update && \
    apt install -y \
    git zip unzip vim curl \
    default-mysql-client \
    libzip-dev zlib1g-dev libpng-dev libjpeg62-turbo-dev libwebp-dev && \
    pecl install xdebug && \
    docker-php-ext-configure gd --with-jpeg --with-webp && \
    docker-php-ext-install pdo_mysql bcmath gd zip && \
    docker-php-enable xdebug
    
WORKDIR /var/src