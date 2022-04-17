FROM php:7.4-fpm

RUN apt update \
    && apt install -y zlib1g-dev g++ git libxml2-dev libicu-dev zip libzip-dev \
    && docker-php-ext-install opcache pdo pdo_mysql xml bcmath \
    && pecl install xdebug-2.9.0 \
    && pecl install apcu \
    && docker-php-ext-enable xdebug apcu \
    && docker-php-ext-configure zip \
    && docker-php-ext-install zip

WORKDIR /var/www/symfonyKubernates

RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

RUN curl -sS https://get.symfony.com/cli/installer | bash
RUN mv /root/.symfony/bin/symfony /usr/local/bin/symfony

##### add code to the container
COPY . /var/www/symfonyKubernates
WORKDIR /var/www/symfonyKubernates

RUN mkdir -p /var/www/symfonyKubernates/var && mkdir -p /var/log/apps
RUN chown -R www-data:www-data /var/www/symfonyKubernates/var && chown -R www-data:www-data /var/log/apps
