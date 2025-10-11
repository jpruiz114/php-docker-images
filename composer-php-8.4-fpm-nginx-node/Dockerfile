FROM node:bullseye AS node_stage

FROM php:8.4-fpm
COPY --from=node_stage /usr/local/ /usr/local/

LABEL maintainer="jpruiz114@gmail.com"

RUN apt-get update && apt-get install -y 7zip git libzip-dev nginx procps supervisor unzip && rm -rf /var/lib/apt/lists/*
RUN docker-php-ext-install zip
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer
COPY config/nginx.conf /etc/nginx/nginx.conf
COPY config/supervisord.conf /etc/supervisor/conf.d/supervisord.conf
WORKDIR /var/www/html
EXPOSE 80
CMD ["supervisord", "-c", "/etc/supervisor/conf.d/supervisord.conf"]
