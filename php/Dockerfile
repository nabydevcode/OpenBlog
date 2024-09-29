FROM php:8.2-apache

# Mise à jour et installation des paquets nécessaires
RUN apt-get update \
    && apt-get install -y \
    build-essential \
    curl \
    zlib1g-dev \
    g++ \
    git \
    libicu-dev \
    zip \
    libzip-dev \
    libpng-dev \
    libjpeg-dev \
    libwebp-dev \
    libfreetype6-dev \
    # Extensions PHP
    && docker-php-ext-install intl opcache pdo pdo_mysql \
    && pecl install apcu \
    && docker-php-ext-enable apcu \
    && docker-php-ext-configure zip \
    && docker-php-ext-install zip \
    && docker-php-ext-configure gd --with-freetype --with-webp --with-jpeg \
    && docker-php-ext-install gd exif

# Activation des modules Apache
RUN a2enmod rewrite ssl socache_shmcb

# Changement de répertoire de travail
WORKDIR /var/www

# Installation de Composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

# Installation de Symfony CLI (correction du chemin)
RUN curl -sS https://get.symfony.com/cli/installer | bash \
    && mv /root/.symfony5/bin/symfony /usr/local/bin/symfony

# Configuration Git
RUN git config --global user.email "condenabytoure123@gmail.com" \
    && git config --global user.name "nabydevcode"
