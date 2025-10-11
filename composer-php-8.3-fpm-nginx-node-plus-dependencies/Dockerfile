FROM docker.io/jpruiz114/composer-php-8.3-fpm-nginx-node:latest

LABEL maintainer="jpruiz114@gmail.com"

# Updates package index and installs specified packages without prompt interruptions.
# build-essential: Installs development tools for compiling software.
# curl: Installs curl for data transfers, useful for testing API endpoints.
# gifsicle: Adds tool for optimizing GIF images.
# jpegoptim: Installs JPEG optimization tool for compressing JPEG images.
# libfreetype6-dev: Adds development libraries for FreeType, supporting font rendering.
# libjpeg-dev: Installs libraries for JPEG image processing.
# libonig-dev: Adds libraries for Oniguruma regex, often required by PHP applications.
# libpng-dev: Installs development libraries for PNG image support.
# libssl-dev: Provides libraries and headers for compiling OpenSSL-based secure software.
# locales: Installs localization files for language and regional support.
# net-tools: Provides network utilities like ifconfig for troubleshooting. (Excluded from the production Dockerfile).
# optipng: Installs PNG optimizer to compress PNG files.
# pngquant: Adds PNG quantization tool for compressing PNG images.
# sudo: Installs sudo to run commands with elevated permissions. (Excluded from the production Dockerfile).
# vim: Adds vim editor for editing files within the container. (Excluded from the production Dockerfile).
# zip: Installs zip utility for compressing files.
# Configures PHP gd extension for FreeType and JPEG support.
# Installs PHP gd extension with concurrent jobs based on CPU cores.

RUN apt-get update && apt-get install -y \
    build-essential \
    curl \
    gifsicle \
    jpegoptim \
    libfreetype6-dev \
    libjpeg-dev \
    libonig-dev \
    libpng-dev \
    libssl-dev \
    locales \
    net-tools \
    optipng \
    pngquant \
    sudo \
    vim \
    zip \
    && docker-php-ext-configure gd --with-freetype --with-jpeg \
    && docker-php-ext-install -j$(nproc) gd

RUN pecl install redis && docker-php-ext-enable redis

# exif: Supports reading metadata from images, like date, time, and camera info. Useful for photo-related apps.
# mbstring: Provides multibyte character handling, especially for languages like Japanese, Chinese, or Korean.
# pcntl: Enables asynchronous signal handling and process control, commonly used in CLI applications.
# pdo: Provides PHP Data Objects, a database access layer abstraction required for PDO database drivers.
# pdo_mysql: Adds MySQL support to PDO, enabling interaction with MySQL databases.
# zip: Enables ZIP archive handling, allowing PHP apps to read and write ZIP files.

RUN docker-php-ext-install exif mbstring pcntl pdo pdo_mysql zip

# Clear cache
RUN apt-get clean && rm -rf /var/lib/apt/lists/*
