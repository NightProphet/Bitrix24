FROM php:7.2-apache

LABEL maintainer="n.p.github@gmail.com"

COPY resources /var/www/html

COPY --from=mlocati/php-extension-installer /usr/bin/install-php-extensions /usr/local/bin/

WORKDIR /var/www/html

RUN chown -R www-data /var/www/html \
    && chmod -R 755 /var/www/html \
    && chmod -R 644 /var/www/html/*

RUN apt update && apt install -y apache2-utils \
    && a2enmod rewrite \
    && service apache2 restart

RUN apt update && apt install -y libfreetype6-dev \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include \
    && docker-php-ext-install -j$(nproc) gd mysqli opcache \
    && install-php-extensions ldap
