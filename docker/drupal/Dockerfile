ARG DRUPAL_IMAGE_FLAVOR=9-php8.0-apache-buster

FROM drupal:${DRUPAL_IMAGE_FLAVOR}

# BCMath (pour Drupal commerce)
RUN docker-php-ext-install -j "$(nproc)" bcmath

# GD (avec prise en charge webp)
RUN apt-get update && apt-get install -y libjpeg-dev libpng-dev libfreetype6-dev libwebp-dev mariadb-client \
    && docker-php-ext-configure gd --with-freetype --with-jpeg --with-webp \
    && docker-php-ext-install gd \
    && rm -rf /var/lib/apt/lists/*

# Ajout de Zsh
RUN apt-get update && apt-get install -y zsh \
    && chsh -s /bin/zsh \
    && ln -sf /bin/zsh /bin/sh

# Instalation de Git
RUN apt-get update && apt-get install -y git

# Install Drush using Composer.
RUN composer require drush/drush:"^11" --prefer-dist

COPY config.ini /usr/local/etc/php/conf.d/
