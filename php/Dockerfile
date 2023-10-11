FROM php:8.1-apache

RUN apt-get update \
    && apt-get install -y unzip libpq-dev git \
    && pecl install xdebug \
    && docker-php-ext-enable xdebug \
    && docker-php-ext-install pgsql pdo_pgsql opcache \
    && a2enmod rewrite

COPY --from=composer /usr/bin/composer /usr/bin/composer
COPY php.ini /usr/local/etc/php/
COPY 000-default.conf /etc/apache2/sites-available/

COPY --from=node:18.16 /usr/local/bin /usr/local/bin
COPY --from=node:18.16 /usr/local/lib /usr/local/lib

WORKDIR /var/www/html