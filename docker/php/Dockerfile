FROM php:8-fpm


RUN apt update \
  && apt install -y zlib1g-dev libzip-dev procps \
  && docker-php-ext-install zip mysqli pdo pdo_mysql \
  && pecl install xdebug \
  && docker-php-ext-enable xdebug

RUN apt install -y npm \
    && npm install n -g \
    && n stable

COPY --from=composer:latest /usr/bin/composer /usr/bin/composer


COPY ./docker/php/php.ini /usr/local/etc/php/
COPY ./docker/php/php-fpm.d/ /usr/local/etc/php-fpm.d/


WORKDIR /var/www/html

RUN useradd -m -s /bin/sh -u 1001 nginx

COPY ./src/ ./

RUN chown -R nginx:nginx /var/www/html \
    && chown -R nginx:nginx /var/run/ \
    && chown -R nginx:nginx /var/log/ \
    && chown -R nginx:nginx /usr/local/etc/php-fpm.d/

# USER nginx
