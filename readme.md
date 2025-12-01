PHP Docker images
=====
![Build PHP 8.5 base](https://github.com/matiux/docker-php/actions/workflows/php-fpm-85-trixie-base.yml/badge.svg)
![Build PHP 8.5 dev](https://github.com/matiux/docker-php/actions/workflows/php-fpm-85-trixie-dev.yml/badge.svg)
![Build PHP 8.4 base](https://github.com/matiux/docker-php/actions/workflows/php-fpm-84-bookworm-base.yml/badge.svg)
![Build PHP 8.4 dev](https://github.com/matiux/docker-php/actions/workflows/php-fpm-84-bookworm-dev.yml/badge.svg)
![Build PHP 8.3 base](https://github.com/matiux/docker-php/actions/workflows/php-fpm-83-bookworm-base.yml/badge.svg)
![Build PHP 8.3 dev](https://github.com/matiux/docker-php/actions/workflows/php-fpm-83-bookworm-dev.yml/badge.svg)
![Build PHP 8.2 base](https://github.com/matiux/docker-php/actions/workflows/php-fpm-82-bullseye-base.yml/badge.svg)
![Build PHP 8.2 dev](https://github.com/matiux/docker-php/actions/workflows/php-fpm-82-bullseye-dev.yml/badge.svg)
![Build PHP 8.1 base](https://github.com/matiux/docker-php/actions/workflows/php-fpm-81-bullseye-base.yml/badge.svg)
![Build PHP 8.1 dev](https://github.com/matiux/docker-php/actions/workflows/php-fpm-81-bullseye-dev.yml/badge.svg)
![Build PHP 8.0 base](https://github.com/matiux/docker-php/actions/workflows/php-fpm-80-bullseye-base.yml/badge.svg)
![Build PHP 8.0 dev](https://github.com/matiux/docker-php/actions/workflows/php-fpm-80-bullseye-dev.yml/badge.svg)
![Build PHP 7.4 base](https://github.com/matiux/docker-php/actions/workflows/php-fpm-74-bullseye-base.yml/badge.svg)
![Build PHP 7.4 dev](https://github.com/matiux/docker-php/actions/workflows/php-fpm-74-bullseye-dev.yml/badge.svg)
![Build PHP 7.3 base](https://github.com/matiux/docker-php/actions/workflows/php-fpm-73-bullseye-base.yml/badge.svg)
![Build PHP 7.3 dev](https://github.com/matiux/docker-php/actions/workflows/php-fpm-73-bullseye-dev.yml/badge.svg)
![Build PHP 7.2 base](https://github.com/matiux/docker-php/actions/workflows/php-fpm-72-buster-base.yml/badge.svg)
![Build PHP 7.2 dev](https://github.com/matiux/docker-php/actions/workflows/php-fpm-72-buster-dev.yml/badge.svg)
![Build PHP 7.1 base](https://github.com/matiux/docker-php/actions/workflows/php-fpm-71-buster-base.yml/badge.svg)
![Build PHP 7.1 dev](https://github.com/matiux/docker-php/actions/workflows/php-fpm-71-buster-dev.yml/badge.svg)
![Build PHP 7.0 base](https://github.com/matiux/docker-php/actions/workflows/php-fpm-70-stretch-base.yml/badge.svg)
![Build PHP 7.0 dev](https://github.com/matiux/docker-php/actions/workflows/php-fpm-70-stretch-dev.yml/badge.svg)
![Build PHP 5.6 base](https://github.com/matiux/docker-php/actions/workflows/php-fpm-56-stretch-base.yml/badge.svg)
![Build PHP 5.6 dev](https://github.com/matiux/docker-php/actions/workflows/php-fpm-56-stretch-dev.yml/badge.svg)
![Build PHP 5.3 base](https://github.com/matiux/docker-php/actions/workflows/php-fpm-53-jessie-base.yml/badge.svg)
![Build PHP 5.3 dev](https://github.com/matiux/docker-php/actions/workflows/php-fpm-53-jessie-dev.yml/badge.svg)

## Immagini PHP:
* [PHP 8.5.* fpm - Debian Trixie](php/debian/trixie/8.5/fpm)
* [PHP 8.4.* fpm - Debian Bookworm](php/debian/bookworm/8.4/fpm)
* [PHP 8.3.* fpm - Debian Bookworm](php/debian/bookworm/8.3/fpm)
* [PHP 8.2.* fpm - Debian Bullseye](php/debian/bullseye/8.2/fpm)
* [PHP 8.1.* fpm - Debian Bullseye](php/debian/bullseye/8.1/fpm)
* [PHP 8.0.* fpm - Debian Bullseye](php/debian/bullseye/8.0/fpm)
* [PHP 7.4.* fpm - Debian Bullseye](php/debian/bullseye/7.4/fpm)
* [PHP 7.3.* fpm - Debian Bullseye](php/debian/bullseye/7.3/fpm)
* [PHP 7.2.* fpm - Debian Buster](php/debian/buster/7.2/fpm)
* [PHP 7.1.* fpm - Debian Buster](php/debian/buster/7.1/fpm)
* [PHP 7.0.* fpm - Debian Stretch](php/debian/stretch/7.0/fpm)
* [PHP 5.6.* fpm - Debian Stretch](php/debian/stretch/5.6/fpm)
* [PHP 5.3.29 apache - Debian Jessie](php/debian/jessie/5.3.29/apache)

[Hub pubblico](https://hub.docker.com/r/matiux/php/tags?page=1&ordering=last_updated)

## Istruzioni per generare le build manualmente

#### Immagine base

```bash
docker build \
#--build-arg GITHUB_TOKEN={github-token} \
#--build-arg BITBUCKET_CONSUMER_KEY={bitbucket-consumer-key} \
#--build-arg BITBUCKET_CONSUMER_SECRET={bitbucket-consumer-secret} \
-t matiux/php:fpm-8.1-bullseye-base .
```

#### Immagine dev
```bash
docker build \
-t matiux/php:fpm-8.1-bullseye-dev .
```

## Gestione tag

#### Tag di un'immagine dopo la build:

```bash
docker tag <id_immagine> \
matiux/php:8.0.1-fpm-alpine3.13-base
```

È anche possibile aggiungere più tag contemporaneamente:

```bash
docker build \
-t matiux/php:7.3.5-fpm-alpine3.9-base \
-t latest \
.
```

Se un'immagine ha più tag è possibile rimuovere un tag, in questo modo non verrà cancellata l'immagine ma solo il tag:

```bash
docker rmi matiux/php:7.3.5-fpm-alpine3.9-base
```

#### Rinominare un tag:

```bash
docker tag <id_immagine> <nuovo_tag>
docker tag b7bb3ad94649 matiux/php:7.3.5-fpm-alpine3.9-base
```

## Gestione hub:
* Login: `docker login`
* Push immagine: `docker push matiux/php:8.0.1-fpm-alpine3.13-base`
* Pull immagine: `docker pull matiux/php:8.0.1-fpm-alpine3.13-base`

## Gestione containers con docker-compose (Deprecato):

Il file [dc.sh](./scripts/dc.sh) è uno script che fa da wrapper a docker-compose semplificando l'utilizzo di alcuni comandi.

* `./dc`: Shortcut per `docker-compose ps`
* `./dc up`: Shortcut per `docker-compose up`. (Es. `./dc up -d`)
* `./dc build php`: Esegue il build dell'immagine PHP
* `./dc enter-root`: Entra nel container php come utente `root`
* `./dc enter`: Entra nel container php come utente `utente`
* `./dc down`: Smonta i servizi. (Es. `./dc down -v` per smontare anche i volumi)
* `./dc purge`: Smonta i servizi e cancella anche le immagini dal disco
* `./dc log`: Mette in ascolto sui log sei servizi
* `./dc exec`: Esegue un qualsiasi comando nel container php
* `./dc composer` Da accesso a composer fuori dal container
* `./dc *` (qualsiasi altro comando docker-compose)

Alias utili per la gestione docker:

```bash
dstopall() { docker stop $(docker ps -aq) && docker rm -f $(docker ps -aq) }
alias dstop="./dc stop"
alias denter="./dc enter"
alias dup="./dc up --remove-orphans"
alias dupd="./dc up -d --remove-orphans"
alias ddown="./dc down"
drmi() { docker rmi -f "$1" }
ddangling() { docker images --filter "dangling=true" -q --no-trunc }
drmdangling() { docker rmi $(ddangling) }
alias dsysp="docker system prune --all -f"
```

## .gitignore:

Aggiungere queste righe al file `.gitignore` del progetto

```bash
docker/docker-compose.override.yml
docker/data/shell_history/.zsh_history
```

## Xdebug:

Nelle immagini `dev` di PHP viene creato configurato Xdebug

* Alpine: `/usr/local/etc/php/conf.d/xdebug.ini`
* Ubuntu / Debian: `/etc/php/8.0/mods-available/xdebug.ini`

Dalle immagini php 7.2 c'è Xdebug 3 che ha chiavi di configurazioni diverse

* [Xdebug 2](php/debian/buster/7.1/fpm/dev/conf/xdebug.ini)
* [Xdebug 3](php/debian/bullseye/8.1/fpm/dev/conf/xdebug.ini)

Nel docker file del progetto è necessario eseguire lo script [xdebug-starter.sh](docker/php/conf/xdebug-starter.sh) per settare l'ip dell'host.

```bash
COPY conf/xdebug-starter.sh /usr/local/bin/xdebug-starter
RUN chmod +x /usr/local/bin/xdebug-starter
RUN /usr/local/bin/xdebug-starter
```

#### Xdebug 3
[Opzioni rinominate](https://xdebug.org/docs/upgrade_guide)

## Comandi Docker utili:

* Pulizia totale: `docker system prune -af --volumes`
* Stop di tutti i container: `docker stop $(docker ps -aq)`
* Eliminazione di tutti i container stoppati: `docker rm -f $(docker ps -aq)`
* Eliminazione delle immagini: `docker rmi -f $(docker images -aq)`
* Informazioni sul volume: `docker volume inspect <id_volume>`
* Ottenere l'ip di un container: `docker inspect --format='{{range .NetworkSettings.Networks}}{{.IPAddress}}{{end}}' nomecontainer`

## Configurazioni PHPStorm

[Screenshots configurazioni](doc/xdebug/phpstorm)

## Miscellanea:

* Le cartelle `public` e `docker/php/test` servono a provare la configurazione `docker-compose`
  simulando una document root per il virtual host.
* Le immagini `dev` sono tutte configurate con oh-my-zsh, vim, xdebug e shell history. Il file viene
  creato in `docker/data/shell_history/.zsh_history` ma ovviamente non è versionato.
* Quando si usa un'immagine mysql / mariadb è possibile caricare un dump di un db (compresso o no) mettendolo nella
  cartella `docker/data/db`. Montando il volume nell'apposito entrypoint, in fase di up questo verrà caricato.

```bash
servicemysql:
    image: mysql:5.7.24
    volumes:
        - app_database:/var/lib/mysql
        - ./mysql/custom.cnf:/etc/mysql/conf.d/custom.cnf
        - ./data/db:/docker-entrypoint-initdb.d
```

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