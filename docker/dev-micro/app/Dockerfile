FROM php:7.4-fpm-alpine
ENV APP_ROOT /var/www/app
WORKDIR $APP_ROOT

# Setup UTC+9
RUN apk --update add tzdata && \
    cp /usr/share/zoneinfo/Asia/Tokyo /etc/localtime && \
    apk del tzdata && \
    rm -rf /var/cache/apk/*

# install packages
RUN apk update && \
    apk upgrade && \
    apk add --update --no-cache \
    autoconf \
    bash \
    build-base \
    curl-dev \
    freetype-dev \
    g++ \
    gcc \
    git \
    icu-dev \
    libjpeg-turbo-dev \
    libpng-dev \
    libxml2-dev \
    libxslt-dev \
    make \
    mysql-dev \
    mysql-client \
    openssl \
    py3-pip \
    sudo \
    tzdata \
    vim \
    redis \
    yaml-dev \
    zlib-dev

RUN docker-php-ext-install pdo_mysql soap intl

RUN docker-php-ext-configure gd \
    --with-freetype=/usr/include/ \
    --with-jpeg=/usr/include/ && \
    NPROC=$(grep -c ^processor /proc/cpuinfo 2>/dev/null || 1) && \
    docker-php-ext-install -j${NPROC} gd

# Install awscli
RUN pip install awscli

# PHP
RUN addgroup -S nginx
RUN adduser -S nginx -G nginx
RUN mkdir /var/run/php-fpm
RUN rm -f /usr/local/etc/php-fpm.conf.default
RUN rm -f /usr/local/etc/php-fpm.d/zz-docker.conf
COPY php/php-fpm.conf /usr/local/etc/php-fpm.conf
COPY php/php.ini /usr/local/etc/php/php.ini
COPY php/www.conf /usr/local/etc/php-fpm.d/www.conf

# Install xdebug
RUN pecl install xdebug-3.1.5 redis
RUN docker-php-ext-enable xdebug

# composer install
RUN curl -sS https://getcomposer.org/installer | php -- --version=2.2.6 --install-dir=/usr/bin
RUN mv /usr/bin/composer.phar /usr/bin/composer

CMD ["/usr/local/sbin/php-fpm", "-F"]
