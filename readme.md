PHP Docker images
=====

![Build PHP 8.1 base](https://github.com/matiux/docker-php/actions/workflows/php-fpm-81-bullseye-base.yml/badge.svg)
![Build PHP 8.1 dev](https://github.com/matiux/docker-php/actions/workflows/php-fpm-81-bullseye-dev.yml/badge.svg)
![Build PHP 8.0 dev](https://github.com/matiux/docker-php/actions/workflows/php-fpm-80-bullseye-base.yml/badge.svg)
![Build PHP 8.0 dev](https://github.com/matiux/docker-php/actions/workflows/php-fpm-80-bullseye-dev.yml/badge.svg)
![Build PHP 7.4 dev](https://github.com/matiux/docker-php/actions/workflows/php-fpm-74-bullseye-base.yml/badge.svg)
![Build PHP 7.4 dev](https://github.com/matiux/docker-php/actions/workflows/php-fpm-74-bullseye-dev.yml/badge.svg)
![Build PHP 7.3 dev](https://github.com/matiux/docker-php/actions/workflows/php-fpm-73-bullseye-base.yml/badge.svg)
![Build PHP 7.3 dev](https://github.com/matiux/docker-php/actions/workflows/php-fpm-73-bullseye-dev.yml/badge.svg)
![Build PHP 7.2 dev](https://github.com/matiux/docker-php/actions/workflows/php-fpm-72-buster-base.yml/badge.svg)
![Build PHP 7.2 dev](https://github.com/matiux/docker-php/actions/workflows/php-fpm-72-buster-dev.yml/badge.svg)
![Build PHP 7.1 dev](https://github.com/matiux/docker-php/actions/workflows/php-fpm-71-buster-base.yml/badge.svg)
![Build PHP 7.1 dev](https://github.com/matiux/docker-php/actions/workflows/php-fpm-71-buster-dev.yml/badge.svg)
![Build PHP 7.0 dev](https://github.com/matiux/docker-php/actions/workflows/php-fpm-70-buster-base.yml/badge.svg)
![Build PHP 7.0 dev](https://github.com/matiux/docker-php/actions/workflows/php-fpm-70-buster-dev.yml/badge.svg)

## Immagini PHP:
* [PHP 8.1.* fpm - Debian Bullseye](php/debian/bullseye/8.1/fpm)
* [PHP 8.0.* fpm - Debian Bullseye](php/debian/bullseye/8.0/fpm)
* [PHP 7.4.* fpm - Debian Bullseye](php/debian/bullseye/7.4/fpm)
* [PHP 7.3.* fpm - Debian Bullseye](php/debian/bullseye/7.3/fpm)
* [PHP 7.2.* fpm - Debian Buster](php/debian/buster/7.2/fpm)
* [PHP 7.1.* fpm - Debian Buster](php/debian/buster/7.1/fpm)
* [PHP 7.0.* fpm - Debian Buster](php/debian/jessie/7.0/fpm)

[Hub pubblico](https://hub.docker.com/r/matiux/php/tags?page=1&ordering=last_updated)

## Project autopilot

A partire dalle immagini php 7.0 è stato introdotta la possibilità di utilizzare un bash script per pilotare il progetto.
Questo script si deve chiamare `project` e va creato in `/var/www/app/scripts/project/bin`. Questo path è aggiunto al `$PATH`
di sistema. È presente anche lo script per l'auto complete `/etc/bash_completion.d/project-autocomplete`. Questo script chiama
il comando `project shortlist` per ottenere la lista dei comandi disponibili e permettere quindi l'auto complete. Un esempio di 
script potrebbe essere il seguente:

```shell
#!/usr/bin/env bash

CMD=$1
shift 1

install_dependencies() {
  composer install --prefer-dist --no-progress
}

schema_drop() {
  php bin/console \
    doctrine:schema:drop \
    --force \
    --full-database \
    --no-interaction \
    --env="${APP_RUNTIME_ENV}"
}

migrate() {
  php bin/console \
    doctrine:migrations:migrate \
    --no-interaction \
    --env="${APP_RUNTIME_ENV}"
}

setup() {
  install_dependencies
  schema_drop
  migrate
}

while :; do
  case $CMD in
  setup-test)
    APP_RUNTIME_ENV='test' setup
    break
    ;;
  setup-dev)
    APP_RUNTIME_ENV='dev' setup
    break
    ;;
  shortlist)
    echo \
      setup-test \
      setup-dev
    break
    ;;
  esac
done
```