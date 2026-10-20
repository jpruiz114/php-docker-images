FROM node:bullseye@sha256:8e02bd83fa9cd8bf2334d0edb9bd8ee405fe09433fd81c2ff4229edc63571e9a AS node_stage

FROM php:8.6-rc-fpm@sha256:10c9fdbbd1b977c07baba768ba4d8a4a7d0979590f6888b10cb45f2929913927
COPY --from=node_stage /usr/local/ /usr/local/

LABEL maintainer="jpruiz114@gmail.com"

RUN apt-get update && apt-get install -y 7zip ca-certificates curl git libzip-dev nginx procps supervisor unzip && rm -rf /var/lib/apt/lists/*
RUN docker-php-ext-install zip
RUN set -eux; \
	curl -fsSL https://getcomposer.org/installer -o composer-setup.php; \
	ACTUAL="$(php -r 'echo hash_file("sha384", "composer-setup.php");')"; \
	EXPECTED="$(curl -fsSL https://composer.github.io/installer.sig | tr -d '\n\r')"; \
	test "$ACTUAL" = "$EXPECTED" || (echo "composer installer checksum mismatch" >&2; exit 1); \
	php composer-setup.php --install-dir=/usr/local/bin --filename=composer; \
	rm -f composer-setup.php
COPY config/nginx.conf /etc/nginx/nginx.conf
COPY config/supervisord.conf /etc/supervisor/conf.d/supervisord.conf
WORKDIR /var/www/html
EXPOSE 80
CMD ["supervisord", "-c", "/etc/supervisor/conf.d/supervisord.conf"]
