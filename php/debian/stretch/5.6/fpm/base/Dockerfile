FROM php:5.6-fpm-stretch

MAINTAINER Matteo Galacci <m.galacci@gmail.com>

#ARG PHP_VERSION=$(php -v | grep ^PHP | cut -d' ' -f2)

RUN apt-get update && apt-get install -y --no-install-recommends \
      ca-certificates \
      curl \
      git \
      less \
      libicu-dev \
      libmemcached-dev \
      libmemcached11 \
      libncurses5-dev \
      libxml2 \
      libzip-dev \
      unzip \
      vim \
      zip \
      zlib1g-dev \
    && pecl install -o \
      memcached-2.2.0 \
    && docker-php-ext-enable \
      memcached \
    && docker-php-ext-install -j5 \
        #`-j` è come per make, per usare 5 thread, accelera la compilazione
        #la regola è che è sempre meglio averla più alta del numero di core a disposizione. La sfiga è che non
        #si può parametrizzare, o ti si invalida la cache della build perché Docker vede un'istruzione diversa
        #(se cambi il parametro)
        bcmath \
        intl \
        opcache \
        pdo_mysql \
        zip \
    && apt-get clean \
    && rm -r /var/lib/apt/lists/*

###> Composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer
###> Fine composer

WORKDIR /var/www/app

# php.ini
RUN mv "$PHP_INI_DIR/php.ini-production" "$PHP_INI_DIR/php.ini"

USER www-data