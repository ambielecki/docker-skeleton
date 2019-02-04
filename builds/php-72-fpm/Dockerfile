FROM php:7.2.14-fpm

RUN apt-get update && \
    apt-get upgrade -y

RUN apt-get install -y --force-yes \
    curl \
    git \
    gnupg \
    libgd-dev \
    libzip-dev \
    nano \
    unzip \
    vim \
    zip \
    zlib1g-dev

RUN pecl install xdebug

RUN docker-php-ext-install \
    gd \
    pdo \
    pdo_mysql \
    zip \
    && docker-php-ext-enable xdebug

RUN docker-php-ext-configure gd --with-freetype-dir=/usr/ --with-jpeg-dir=/usr/ --with-png-dir=/usr/  &&  \
    docker-php-ext-install gd

# Install latest node and npm
RUN  apt-get update -yq \
    && curl -sL https://deb.nodesource.com/setup_10.x | bash \
    && apt-get install nodejs -yq

# Install composer
ENV COMPOSER_ALLOW_SUPERUSER=1
RUN curl -sS https://getcomposer.org/installer | php && \
    mv composer.phar /usr/local/bin/composer && \
    printf "\nPATH=\"~/.composer/vendor/bin:\$PATH\"\n" | tee -a ~/.bashrc

COPY ./xdebug.ini /usr/local/etc/php/conf.d/xdebug.ini