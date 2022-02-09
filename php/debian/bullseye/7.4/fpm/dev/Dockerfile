FROM matiux/php:fpm-7.4-bullseye-base

MAINTAINER Matteo Galacci <m.galacci@gmail.com>

USER root

RUN apt-get update \
    && apt-get install -y --no-install-recommends \
    awscli \
    curl \
    default-mysql-client \
    git \
    iproute2 \
    locales \
    locales-all \
    mycli \
    nano \
    rsync \
    tzdata \
    ssh \
    sudo \
    vim \
    wget \
    zsh

###> Configurazioni e permessi
ENV TZ=Europe/Rome
RUN locale-gen en_US.UTF-8

RUN echo 'memory_limit = 2048M' >> "$PHP_INI_DIR/conf.d/docker-php-memlimit.ini" \
    && chown -R www-data:www-data /var/www \
    && groupadd -g 1000 utente \
    && useradd -m -u 1000 -g www-data utente \
    && usermod -aG www-data utente

COPY conf/sudo-DEV /etc/sudoers.d/DEV
###> Fine configurazioni e permessi

###> Configurazione Xdebug
ENV XDEBUG_CONF_FILE=$PHP_INI_DIR/conf.d/docker-php-ext-xdebug.ini
ENV PHP_IDE_CONFIG=serverName=application
RUN chown utente:utente /usr/local/etc/php/conf.d/
COPY --chown=www-data:www-data conf/xdebug.ini $XDEBUG_CONF_FILE

RUN apt-get install -y --no-install-recommends \
    && pecl install xdebug-3.1.3 \
    && docker-php-ext-enable xdebug
###> Fine configurazione Xdebug

###> Zsh
RUN apt-get install -y --no-install-recommends \
    locales

RUN locale-gen en_US.UTF-8
ENV LANG en_US.UTF-8
ENV LANGUAGE en_US:en
ENV LC_ALL en_US.UTF-8

USER utente

RUN wget https://github.com/robbyrussell/oh-my-zsh/raw/master/tools/install.sh -O - | zsh || true

COPY --chown=utente:utente conf/zshrc /home/utente/.zshrc

COPY --chown=utente:utente conf/custom-agnoster.zsh-theme /home/utente/.oh-my-zsh/custom/themes/custom-agnoster.zsh-theme
RUN sed -i "s/ZSH_THEME=\"robbyrussell\"/ZSH_THEME=\"custom-agnoster\"/" ~/.zshrc \
    && echo "\nexport DEFAULT_USER=utente" >> ~/.zshrc
###> Fine zsh

###> Configurazione aws-vault e plugin zsh dentro al container
RUN sudo curl -L -o /usr/local/bin/aws-vault https://github.com/99designs/aws-vault/releases/download/v6.5.0/aws-vault-linux-amd64
RUN sudo chmod 755 /usr/local/bin/aws-vault

RUN git clone https://github.com/blimmer/zsh-aws-vault.git ~/.oh-my-zsh/custom/plugins/zsh-aws-vault \
    && sed -i.bak 's/^plugins=(\(.*\)/plugins=(zsh-aws-vault \1/' ~/.zshrc
###> Fine configurazione aws-vault e plugin zsh dentro al container

###> Configurazione Zsh Autosuggestions
RUN git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions \
    && sed -i.bak 's/^plugins=(\(.*\)/plugins=(zsh-autosuggestions \1/' ~/.zshrc \
    && echo "export ZSH_AUTOSUGGEST_HIGHLIGHT_STYLE=\"fg=#0cb074\"" >> ~/.zshrc
###> Fine configurazione Zsh Autosuggestions

###> Shell
COPY conf/project-autocomplete /etc/bash_completion.d

COPY --chown=utente:utente conf/shell-custom.rc /tmp/shell-custom.rc
RUN echo "" >> /tmp/shell-custom.rc \
    && cat /tmp/shell-custom.rc >> /home/utente/.zshrc  \
    && cat /tmp/shell-custom.rc >> /home/utente/.bashrc
###> Fine Shell

###> Pulizia
USER root

RUN apt-get remove --purge -y software-properties-common \
    && apt-get autoremove -y \
    && apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*
###> Fine pulizia

USER www-data