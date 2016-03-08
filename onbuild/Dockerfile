FROM php:fpm

# Environmental Variables
ENV COMPOSER_HOME /root/composer
ENV PATH $COMPOSER_HOME/vendor/bin:$PATH

# APT Setup
COPY hhvm.list /etc/apt/sources.list.d/hhvm.list
RUN apt-key adv --recv-keys --keyserver hkp://keyserver.ubuntu.com:80 0x5a16e7281be7a449

RUN apt-get update && \
  DEBIAN_FRONTEND=noninteractive apt-get install -y \
    libfreetype6-dev \
    libjpeg62-turbo-dev \
    libmcrypt-dev \
    libpng12-dev \
    libbz2-dev \
    php-pear \
    curl \
    git \
    subversion \
    unzip \
    hhvm \
  && rm -r /var/lib/apt/lists/*

# PHP Extensions
RUN docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
  && docker-php-ext-install gd mcrypt zip bz2 mbstring

# Memory Limit
RUN echo "memory_limit=-1" > $PHP_INI_DIR/conf.d/memory-limit.ini

# Set up the application directory
RUN mkdir -p /usr/src/app && \
    ln -s /usr/src/app /app
WORKDIR /usr/src/app

# Onbuild Install
ONBUILD RUN echo "date.timezone=${PHP_TIMEZONE:-UTC}" > $PHP_INI_DIR/conf.d/date_timezone.ini &&
    curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

ONBUILD COPY composer.json /usr/src/app/
ONBUILD RUN hhvm /usr/local/bin/composer --ansi install
ONBUILD COPY . /usr/src/app/
