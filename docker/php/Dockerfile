FROM php:7.4.33-fpm-alpine

ARG UID
ARG GID

RUN apk --no-cache update && apk add --no-cache build-base \
    openssl-dev \
    freetype-dev \
    libjpeg-turbo-dev \
    libpng-dev \
    libxml2-dev \
    libzip-dev \
    oniguruma-dev \
    zlib-dev \
    jpeg-dev \
    autoconf \
    shadow \
    sudo

RUN apk del build-base openssl-dev autoconf

RUN groupadd -g ${GID} container && useradd -m -u ${UID} -g container admin

RUN echo "admin ALL=(ALL) NOPASSWD: ALL" > /etc/sudoers.d/admin && chmod 0440 /etc/sudoers.d/admin

RUN docker-php-ext-configure gd --with-jpeg --with-freetype

RUN docker-php-ext-install pdo mysqli pdo_mysql xml mbstring zip gd

WORKDIR /var/www/html

RUN chown -R admin:container .

USER admin

EXPOSE 9000

CMD [ "php-fpm" ]
