FROM php:5-fpm

RUN apt-get update && apt-get install -y libmcrypt-dev
RUN docker-php-ext-install mbstring mcrypt pdo pdo_mysql

RUN mkdir -p /usr/local/etc/php/conf.d

WORKDIR /app
