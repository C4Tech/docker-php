FROM php:5-fpm

RUN apt-get update && apt-get install -y libmcrypt-dev
RUN docker-php-ext-install mbstring mcrypt

RUN mkdir -p /usr/local/etc/php/conf.d
COPY upload.ini /usr/local/etc/php/conf.d/10-upload.ini

CMD ["php-fpm"]
