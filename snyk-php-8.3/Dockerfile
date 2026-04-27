FROM node:bullseye@sha256:8e02bd83fa9cd8bf2334d0edb9bd8ee405fe09433fd81c2ff4229edc63571e9a AS node_stage

LABEL maintainer="jpruiz114@gmail.com"

RUN npm install -g snyk-to-html@3.7.1
RUN npm install -g snyk@1.1304.0

FROM php:8.3-cli@sha256:92ff31bbd049fd199bf3700719374e4594b2baa7324eefc459bda26d622c3ea9
COPY --from=node_stage /usr/local/ /usr/local/
RUN apt-get update && apt-get install -y ca-certificates curl zip unzip
RUN set -eux; \
	curl -fsSL https://getcomposer.org/installer -o composer-setup.php; \
	ACTUAL="$(php -r 'echo hash_file("sha384", "composer-setup.php");')"; \
	EXPECTED="$(curl -fsSL https://composer.github.io/installer.sig | tr -d '\n\r')"; \
	test "$ACTUAL" = "$EXPECTED" || (echo "composer installer checksum mismatch" >&2; exit 1); \
	php composer-setup.php --install-dir=/usr/local/bin --filename=composer; \
	rm -f composer-setup.php
