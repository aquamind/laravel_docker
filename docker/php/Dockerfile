FROM php:7.4-fpm
COPY php.ini /usr/local/etc/php/

RUN apt-get update \
  && apt-get install -y zlib1g-dev libzip-dev mariadb-client unzip\
  && docker-php-ext-install zip pdo_mysql

RUN pecl install xdebug \
    && docker-php-ext-enable xdebug

#Composer install
COPY --from=composer:1.10.20 /usr/bin/composer /usr/bin/composer

ENV COMPOSER_ALLOW_SUPERUSER 1
ENV COMPOSER_HOME /composer
ENV PATH $PATH:/composer/vendor/bin

WORKDIR /var/www
RUN composer global require "laravel/installer"
