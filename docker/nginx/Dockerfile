FROM nginx:latest

RUN apt update \
    && apt install -y vim procps

COPY ./conf.d/ /etc/nginx/conf.d/
COPY ./nginx.conf /etc/nginx/nginx.conf

RUN groupadd -g 1001 www-user && usermod -aG www-user nginx
RUN groupadd -g 1002 uwsgi && usermod -aG uwsgi nginx

RUN mkdir /var/run/nginx
RUN chown -R nginx:nginx /var/cache/nginx /etc/nginx /var/run/nginx /var/log/nginx

USER nginx

CMD ["nginx", "-g", "daemon off;"]
