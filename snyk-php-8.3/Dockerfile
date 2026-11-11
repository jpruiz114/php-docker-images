FROM node:26-trixie-slim@sha256:5adad64f9a1fca2d51972caa65983634c8a774eb300d72b20f7f2a0f60368072 AS node_stage
# Upgrade the npm bundled with Node to pick up fixes in its dependencies (undici, brace-expansion).
RUN npm install -g npm@11.21.2

LABEL maintainer="jpruiz114@gmail.com"

RUN npm install -g snyk-to-html@3.7.11
RUN npm install -g snyk@1.1308.4

FROM php:8.3-cli@sha256:628102249d93494233b54490b785f12db9cd60f4dc89416dfca15973f2125f10
COPY --from=node_stage /usr/local/ /usr/local/
RUN apt-get update && apt-get upgrade -y && apt-get install -y ca-certificates curl zip unzip
RUN set -eux; \
	curl -fsSL https://getcomposer.org/installer -o composer-setup.php; \
	ACTUAL="$(php -r 'echo hash_file("sha384", "composer-setup.php");')"; \
	EXPECTED="$(curl -fsSL https://composer.github.io/installer.sig | tr -d '\n\r')"; \
	test "$ACTUAL" = "$EXPECTED" || (echo "composer installer checksum mismatch" >&2; exit 1); \
	php composer-setup.php --install-dir=/usr/local/bin --filename=composer; \
	rm -f composer-setup.php
