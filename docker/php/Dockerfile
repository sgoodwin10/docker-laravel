ARG PHP_VERSION=7.1
FROM php:$PHP_VERSION-fpm

ARG WITH_XDEBUG=0
ENV WITH_XDEBUG $WITH_XDEBUG

ARG GIT_USER
ENV GIT_USER $GIT_USER
ARG GIT_EMAIL
ENV GIT_EMAIL $GIT_EMAIL

# timezone
ARG TZ

# composer
ENV COMPOSER_ALLOW_SUPERUSER 1
ENV COMPOSER_HOME /composer

RUN cp /usr/share/zoneinfo/Australia/Sydney /etc/localtime \
  && echo ${TZ} > /etc/timezone

RUN apt-get update -y && apt-get install -y \
    openssl \
    curl \ 
    wget \
    git \
    libmcrypt-dev \
    mariadb-client \
    mariadb-server \ 
    && docker-php-ext-install mcrypt \ 
    && docker-php-ext-install pdo_mysql \ 
    && docker-php-ext-install mbstring \
    && docker-php-ext-install bcmath \
    && docker-php-ext-install mysqli

RUN apt-get install -y libmagickwand-dev --no-install-recommends \
    && pecl install imagick \
    && docker-php-ext-enable imagick

RUN pecl install xdebug \
    && docker-php-ext-enable xdebug
    
RUN git clone https://github.com/phpredis/phpredis.git /usr/src/php/ext/redis \
    && docker-php-ext-install redis
    
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer 

RUN git config --global user.email "$GIT_EMAIL"
RUN git config --global user.name "$GIT_USER"


