FROM php:fpm

# For composer
RUN apt-get update && apt-get install -y \
    zlib1g-dev \
    libzip-dev \
    git \
    unzip\
    vim \
    && docker-php-ext-install \
    zip \
    && apt-get clean

# Install composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

# Set composer environment
ENV COMPOSER_ALLOW_SUPERUSER 1
ENV COMPOSER_HOME /composer
ENV PATH $PATH:/composer/vendor/bin

# Install laravel installer
RUN composer global require "laravel/installer"

# PHP's DB setting
RUN apt-get update \
    && apt-get install -y libpq-dev \
    && docker-php-ext-install pdo_mysql

WORKDIR /src
