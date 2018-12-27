FROM php:7.1-apache

# Install common tools and libraries
RUN apt-get update && apt-get install -y --no-install-recommends \
    curl \
    git \
    zip \
    unzip \
    vim \
    openssl \
    libz-dev \
    libjpeg-dev \
    libmcrypt-dev \
    autoconf \
    file \
    g++ \
    gcc

# Installed PHP extensions
RUN apt-get install -y libmcrypt-dev mysql-client libmagickwand-dev --no-install-recommends \
    && pecl install imagick \
    && docker-php-ext-enable imagick \
    && docker-php-ext-install mcrypt pdo_mysql

# Enable apache re-write and SSL modules
RUN a2enmod rewrite \
    && a2enmod ssl

# Cleanup
RUN apt-get clean

# Install composer
RUN curl -sS https://getcomposer.org/installer | \
    php -- --install-dir=/usr/local/bin --filename=composer

# Adding virtual host file
ADD config/000-default.conf /etc/apache2/sites-enabled/000-default.conf

# Adding custom php configuration file
ADD config/php.ini /usr/local/etc/php/conf.d/custom.ini

# Set working directory
WORKDIR /var/www/html
