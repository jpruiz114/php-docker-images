FROM php:8.6-rc-cli@sha256:58c17b6ac3bcdbe40935ca738ab0f587271e396446a26805e7be9367257f84e9

LABEL maintainer="jpruiz114@gmail.com"

# PHP 8.6 images no longer ship PECL/PEAR; PIE (PHP Installer for Extensions) is the official replacement.
COPY --from=ghcr.io/php/pie:1.5.2-bin@sha256:a254c78b51ca34daef0541fa1cf0147385c93ba5ca799868392275d947f00fe7 /pie /usr/bin/pie

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
# Xdebug 3.6 is the first release line supporting PHP 8.6 (still alpha at the time of writing).
RUN pie install xdebug/xdebug:3.6.0alpha1

# Install Redis extension and enable it
# Stable phpredis (6.3.0) does not compile against PHP 8.6; pinned to a develop commit until a compatible release is tagged.
RUN pie install phpredis/phpredis:dev-develop#4366a579e52a35a6150e2c0e61c1c3a89c6f8484

# Configure Xdebug for code coverage
RUN echo "xdebug.mode=coverage" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini
