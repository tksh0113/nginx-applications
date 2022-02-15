FROM php:8-fpm

RUN apt update \
    && apt install -y zlib1g-dev libzip-dev procps vim \
    && docker-php-ext-install zip mysqli pdo pdo_mysql \
    && pecl install xdebug \
    && docker-php-ext-enable xdebug

COPY ./docker/php/php.ini /usr/local/etc/php/
COPY ./docker/php/php-fpm.d/ /usr/local/etc/php-fpm.d/

RUN useradd -m -s /bin/sh -u 1001 www-user

RUN mkdir /var/run/php-fpm
RUN chown -R www-user:www-user /var/www/ /var/run/php-fpm /usr/local/etc/php-fpm.d/

WORKDIR /var/www/html

COPY ./src/ ./

USER www-user
