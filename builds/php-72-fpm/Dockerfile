FROM php:7.2.14-fpm

RUN apt-get update \
    && apt-get upgrade -y \
    && curl -sL https://deb.nodesource.com/setup_10.x | bash \

RUN apt-get install -y --force-yes \
    curl \
    git \
    gnupg \
    libgd-dev \
    libzip-dev \
    nano \
    nodejs \
    unzip \
    vim \
    zip \
    zlib1g-dev

RUN pecl install xdebug

RUN docker-php-ext-configure gd --with-freetype-dir=/usr/ --with-jpeg-dir=/usr/ --with-png-dir=/usr/

RUN docker-php-ext-install \
    gd \
    pdo \
    pdo_mysql \
    zip \
    && docker-php-ext-enable xdebug

# Install composer
ENV COMPOSER_ALLOW_SUPERUSER=1
RUN curl -sS https://getcomposer.org/installer | php \
    && mv composer.phar /usr/local/bin/composer \
    && printf "\nPATH=\"~/.composer/vendor/bin:\$PATH\"\n" | tee -a ~/.bashrc

RUN curl -L https://cs.symfony.com/download/php-cs-fixer-v2.phar -o php-cs-fixer \
    && chmod a+x php-cs-fixer \
    && mv php-cs-fixer /usr/local/bin/php-cs-fixer

COPY ./xdebug.ini /usr/local/etc/php/conf.d/xdebug.ini