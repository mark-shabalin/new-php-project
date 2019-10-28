ARG PHP_IMAGE

FROM ${PHP_IMAGE}

ARG UID
ARG GID

RUN apk --no-cache update \
    && apk --no-cache upgrade

RUN if [ ! -z "$UID" ] && [ ! -z "$GID" ]; then apk add shadow && usermod -u $UID www-data && groupmod -g $GID www-data; fi

RUN apk add --no-cache libzip-dev

RUN apk add --no-cache $PHPIZE_DEPS \
        freetype \
        freetype-dev \
        libjpeg-turbo \
        libjpeg-turbo-dev \
        libpng \
        libpng-dev && \
    docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ --with-png-dir=/usr/include/ && \
    docker-php-ext-install -j$(getconf _NPROCESSORS_ONLN) gd

RUN set -ex \
    && apk add --no-cache --virtual .phpize-deps $PHPIZE_DEPS imagemagick-dev libtool \
    && export CFLAGS="$PHP_CFLAGS" CPPFLAGS="$PHP_CPPFLAGS" LDFLAGS="$PHP_LDFLAGS" \
    && pecl install imagick-3.4.3 \
    && docker-php-ext-enable imagick \
    && apk add --no-cache --virtual .imagick-runtime-deps imagemagick \
    && apk del .phpize-deps

RUN docker-php-ext-install mysqli pdo pdo_mysql zip bcmath

RUN apk add --no-cache git

RUN apk add --no-cache composer

RUN apk add --no-cache mysql-client

RUN apk add --no-cache bash

RUN apk add --no-cache ssmtp
