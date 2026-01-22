FROM php:8.5-fpm-trixie

LABEL maintainer="Matteo Galacci <m.galacci@gmail.com>"

# Install system dependencies & PHP extensions
RUN apt-get update \
    && apt-get install -y --no-install-recommends \
        ca-certificates \
        curl \
        libicu-dev \
        libxml2 \
        libzip-dev \
        unzip \
        zip \
        zlib1g-dev \
    && docker-php-ext-install -j"$(nproc)" \
        bcmath \
        intl \
        pdo_mysql \
        zip \
    && apt-get purge -y --auto-remove \
    && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

RUN mv "$PHP_INI_DIR/php.ini-production" "$PHP_INI_DIR/php.ini"

# Copy OPcache configuration
COPY conf/opcache.ini /usr/local/etc/php/conf.d/opcache.ini

WORKDIR /var/www/app

USER www-data
