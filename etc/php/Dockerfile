FROM php:7.4-fpm

# Download script to install PHP extensions and dependencies
ADD https://raw.githubusercontent.com/mlocati/docker-php-extension-installer/master/install-php-extensions /usr/local/bin/

RUN chmod uga+x /usr/local/bin/install-php-extensions && sync

RUN DEBIAN_FRONTEND=noninteractive apt-get update -q \
  && DEBIAN_FRONTEND=noninteractive apt-get install -qq -y \
  curl \
  git \
  zip unzip \
  && install-php-extensions \
  bcmath \
  bz2 \
  calendar \
  exif \
  gd \
  intl \
  ldap \
  memcached \
  mysqli \
  opcache \
  pdo_mysql \
  pdo_pgsql \
  pgsql \
  redis \
  soap \
  xsl \
  zip \
  sockets

# Install git
RUN apt-get update \
  && apt-get -y install git \
  && apt-get clean; rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* /usr/share/doc/*

# Install Composer.
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer \
  && ln -s $(composer config --global home) /root/composer

ENV PATH=$PATH:/root/composer/vendor/bin COMPOSER_ALLOW_SUPERUSER=1

RUN composer global require hirak/prestissimo

# Install Node
RUN apt-get update &&\
  apt-get install -y --no-install-recommends gnupg && \
  curl -sL https://deb.nodesource.com/setup_14.x | bash - && \
  apt-get update && \
  apt-get install -y --no-install-recommends nodejs && \
  npm install --global gulp-cli

WORKDIR /var/www/html
