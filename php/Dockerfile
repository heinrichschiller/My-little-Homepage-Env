FROM php:8.0-apache

# Install packages
RUN apt-get update && \
 apt-get install -y \
  curl \
  unzip \
  git \
  && \
  apt-get clean -y && \
  rm -rf /var/cache/apt /var/lib/apt/lists/*

RUN pecl install xdebug \
 && docker-php-ext-enable xdebug

# Install PHP extensions
# RUN docker-php-ext-install pdo_mysql

# Add Apache mod_rewrite
RUN a2enmod rewrite

# Install Composer
RUN curl -sS https://getcomposer.org/installer \
 | php -- --install-dir=/usr/bin --filename=composer

COPY app/ /var/www/html/
COPY php/conf.d/error_reporting.ini /usr/local/etc/php/conf.d/docker-php-ext-error_reporting.ini
COPY php/conf.d/xdebug.ini /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini

# Set workdir
WORKDIR /var/www/html/
