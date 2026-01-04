FROM node:bullseye AS node_stage

LABEL maintainer="jpruiz114@gmail.com"

RUN npm install snyk-to-html -g
RUN npm install -g snyk@latest

FROM php:8.5-cli
COPY --from=node_stage /usr/local/ /usr/local/
RUN apt-get update && apt-get install -y zip unzip
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer
