FROM node:26-trixie-slim@sha256:5adad64f9a1fca2d51972caa65983634c8a774eb300d72b20f7f2a0f60368072 AS node_stage
# Upgrade the npm bundled with Node to pick up fixes in its dependencies (undici, brace-expansion).
RUN npm install -g npm@11.21.2

FROM php:8.4-fpm@sha256:212c3c9fc09d58f6b1a12b0b4a6a90fd44a209299a67633c2bccbc1dd53c55e0
COPY --from=node_stage /usr/local/ /usr/local/

LABEL maintainer="jpruiz114@gmail.com"

RUN apt-get update && apt-get upgrade -y && apt-get install -y 7zip ca-certificates curl git libzip-dev nginx procps supervisor unzip && rm -rf /var/lib/apt/lists/*
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
