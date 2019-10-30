FROM php:7.1.5-apache

COPY ./php/php.ini /usr/local/etc/php/
COPY ./apache/*.conf /etc/apache2/sites-enabled/

RUN apt-get update && \
    apt-get install -y --no-install-recommends \
        curl apt-utils mysql-client zip unzip \
        # for gd
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libpng-dev \
        libwebp-dev \
        libxpm-dev \
        # for ImageMagick
        libmagickwand-dev \
        # for intl
        libicu-dev \
        # from zip
        zlib1g-dev && \
    pecl install imagick && \
    docker-php-ext-enable imagick && \
    docker-php-ext-install \
        bcmath \
        intl \
        mbstring \
        mysqli \
        pdo_mysql \
        zip \
        gettext && \
    docker-php-ext-install -j$(nproc) iconv && \
    docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ && \
    docker-php-ext-install -j$(nproc) gd && \
    rm -rf /var/lib/apt/lists/* && \
    apt-get clean && \
    # enable mod_rewrite
    a2enmod rewrite

# node
RUN curl -sL https://deb.nodesource.com/setup_8.x | bash - && \
    apt-get update && \
    apt-get install -y nodejs && \
    npm install npm@latest -g

# composer install
RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" && \
    php composer-setup.php && \
    php -r "unlink('composer-setup.php');" && \
    mv composer.phar /usr/local/bin/composer

ENV COMPOSER_ALLOW_SUPERUSER 1
ENV COMPOSER_HOME /composer
ENV PATH $PATH:/composer/vendor/bin

# Laravel install
# RUN composer global require "laravel/installer"

WORKDIR /var/www/html