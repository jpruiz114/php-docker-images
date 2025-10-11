FROM php:8.3-cli

LABEL maintainer="jpruiz114@gmail.com"

# Install basic dependencies
RUN apt-get update && apt-get install -y zip unzip

# Install Composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

# Install Xdebug and enable it
RUN pecl install xdebug && docker-php-ext-enable xdebug

# Install Redis extension and enable it
RUN pecl install redis && docker-php-ext-enable redis

# Configure Xdebug for code coverage
RUN echo "xdebug.mode=coverage" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini
