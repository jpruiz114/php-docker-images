FROM php:8.4-cli@sha256:c8c4d2165bf3139039094c99c9370ead168df29ffa6c12373268dca212f0c938

LABEL maintainer="jpruiz114@gmail.com"

# Install basic dependencies
RUN apt-get update && apt-get install -y ca-certificates curl zip unzip

# Install Composer
RUN set -eux; \
	curl -fsSL https://getcomposer.org/installer -o composer-setup.php; \
	ACTUAL="$(php -r 'echo hash_file("sha384", "composer-setup.php");')"; \
	EXPECTED="$(curl -fsSL https://composer.github.io/installer.sig | tr -d '\n\r')"; \
	test "$ACTUAL" = "$EXPECTED" || (echo "composer installer checksum mismatch" >&2; exit 1); \
	php composer-setup.php --install-dir=/usr/local/bin --filename=composer; \
	rm -f composer-setup.php

# Install Xdebug and enable it
RUN pecl install xdebug && docker-php-ext-enable xdebug

# Install Redis extension and enable it
RUN pecl install redis && docker-php-ext-enable redis

# Configure Xdebug for code coverage
RUN echo "xdebug.mode=coverage" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini
