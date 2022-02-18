FROM php:8-fpm

RUN apt update \
    && apt install -y zlib1g-dev libzip-dev unzip procps vim \
    && docker-php-ext-install zip

COPY ./php.ini /usr/local/etc/php/
COPY ./php-fpm.d/ /usr/local/etc/php-fpm.d/

RUN useradd -m -s /bin/sh -u 1001 www-user

RUN mkdir /var/run/php-fpm

RUN chown -R www-user:www-user /var/www/ /var/run/php-fpm /usr/local/etc/php-fpm.d/

WORKDIR /var/www/html

USER www-user

COPY --chown=www-user:www-user . .
