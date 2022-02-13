FROM nginx:latest

COPY ./docker/nginx/conf.d/ /etc/nginx/conf.d/
COPY ./docker/nginx/nginx.conf /etc/nginx/nginx.conf

RUN useradd -m -s /bin/sh -u 1001 nginx_docker

#RUN chown -R nginx:nginx /var/www/html \
#    && chown -R nginx:nginx /var/run/ \
#    && chown -R nginx:nginx /var/log/ \
#    && chown -R nginx:nginx /usr/local/etc/php-fpm.d/

#USER nginx
