FROM php:7.4-fpm-alpine

WORKDIR /var/www/html

RUN apk update && apk add --no-cache \
    build-base shadow vim curl \
    php7 \
    php7-fpm \
    php7-common \
    php7-pdo \
    php7-pdo_mysql \
    php7-mysqli \
    php7-mcrypt \
    php7-mbstring \
    php7-xml \
    php7-openssl \
    php7-json \
    php7-phar \
    php7-zip \
    php7-gd \
    php7-dom \
    php7-session \
    php7-zlib

RUN docker-php-ext-install pdo pdo_mysql mysqli
RUN docker-php-ext-enable pdo_mysql

# Install Composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer
#RUN pecl install xdebug-2.5.0 \ && docker-php-ext-enable xdebug
#RUN echo xdebug.remote_enable=1 >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini \
#    && echo xdebug.remote_port=9000 >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini \
#    && echo xdebug.remote_autostart=1 >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini \
#    && echo xdebug.remote_connect_back=0 >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini \
#    && echo xdebug.idekey=PHP_STORM >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini \
#    && echo xdebug.remote_host=host.docker.internal >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini

RUN rm -rf /var/cache/apk/*
RUN usermod -u 1000 www-data
COPY --chown=www-data:www-data . /var/www/html
USER www-data
EXPOSE 9000
CMD ["php-fpm"]
