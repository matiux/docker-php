# Stage composer (pinnato, niente latest)
FROM composer:2.9 AS composer_bin

FROM matiux/php:fpm-8.5-trixie-base

LABEL maintainer="Matteo Galacci <m.galacci@gmail.com>"

USER root

#
# ---------------------------------------------------------
# 0. Composer (dev)
# ---------------------------------------------------------
#
ENV COMPOSER_HOME=/tmp/composer
COPY --from=composer_bin /usr/bin/composer /usr/local/bin/composer


#
# ---------------------------------------------------------
# 1. Pacchetti development
# ---------------------------------------------------------
#
RUN apt-get update \
 && apt-get install -y --no-install-recommends \
    awscli \
    bash-completion \
    curl \
    default-mysql-client \
    git \
    iproute2 \
    locales \
    mycli \
    nano \
    rsync \
    ssh \
    sudo \
    tzdata \
    vim \
    wget \
    zsh \
 && locale-gen en_US.UTF-8 \
 && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*


#
# ---------------------------------------------------------
# 2. PHP memory limit
# ---------------------------------------------------------
#
RUN echo 'memory_limit = 2048M' > "$PHP_INI_DIR/conf.d/docker-php-memlimit.ini"


#
# ---------------------------------------------------------
# 3. Users & permissions
# ---------------------------------------------------------
#
# FIX: tolto groupadd (GID 1000 può confliggere)
# Creo utente "utente" con UID 1000 e gruppo primario www-data (già presente nell'immagine php)
RUN useradd -m -u 1000 -g www-data utente \
 && usermod -aG www-data utente \
 && chown -R www-data:www-data /var/www \
 && mkdir -p /tmp/composer \
 && chown -R utente:www-data /tmp/composer

COPY conf/sudo-DEV /etc/sudoers.d/DEV


#
# ---------------------------------------------------------
# 4. XDEBUG installation (only in dev)
# ---------------------------------------------------------
#
ENV XDEBUG_CONF_FILE=$PHP_INI_DIR/conf.d/docker-php-ext-xdebug.ini
ENV PHP_IDE_CONFIG=serverName=application

COPY --chown=www-data:www-data conf/xdebug.ini $XDEBUG_CONF_FILE

RUN apt-get update \
 && apt-get install -y --no-install-recommends $PHPIZE_DEPS \
 && pecl install xdebug-3.5.0 \
 && docker-php-ext-enable xdebug \
 && apt-get purge -y --auto-remove $PHPIZE_DEPS \
 && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*


#
# ---------------------------------------------------------
# 5. ZSH + Oh-my-zsh
# ---------------------------------------------------------
#
USER utente

RUN sh -c "$(wget -O- https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)" || true

COPY --chown=utente:utente conf/zshrc /home/utente/.zshrc
COPY --chown=utente:utente conf/custom-agnoster.zsh-theme /home/utente/.oh-my-zsh/custom/themes/custom-agnoster.zsh-theme
RUN sed -i 's/ZSH_THEME="robbyrussell"/ZSH_THEME="custom-agnoster"/' ~/.zshrc \
 && echo "\nexport DEFAULT_USER=utente" >> ~/.zshrc

#
# ---------------------------------------------------------
# 6. Plugins ZSH (aws-vault + autosuggestions)
# ---------------------------------------------------------
#
USER root
RUN curl -L -o /usr/local/bin/aws-vault https://github.com/99designs/aws-vault/releases/download/v6.5.0/aws-vault-linux-amd64 \
 && chmod 755 /usr/local/bin/aws-vault
USER utente

RUN git clone https://github.com/blimmer/zsh-aws-vault.git ~/.oh-my-zsh/custom/plugins/zsh-aws-vault \
 && sed -i.bak 's/^plugins=(\(.*\)/plugins=(zsh-aws-vault \1/' ~/.zshrc

RUN git clone https://github.com/zsh-users/zsh-autosuggestions ~/.oh-my-zsh/custom/plugins/zsh-autosuggestions \
 && sed -i.bak 's/^plugins=(\(.*\)/plugins=(zsh-autosuggestions \1/' ~/.zshrc \
 && echo "export ZSH_AUTOSUGGEST_HIGHLIGHT_STYLE=\"fg=#0cb074\"" >> ~/.zshrc

#
# ---------------------------------------------------------
# 7. Autocomplete
# ---------------------------------------------------------
#
COPY conf/project-autocomplete /etc/bash_completion.d

#
# ---------------------------------------------------------
# 8. Shell custom
# ---------------------------------------------------------
#
COPY --chown=utente:utente conf/shell-custom.rc /tmp/shell-custom.rc
RUN echo "" >> /tmp/shell-custom.rc \
    && cat /tmp/shell-custom.rc >> /home/utente/.zshrc \
    && cat /tmp/shell-custom.rc >> /home/utente/.bashrc

USER utente
