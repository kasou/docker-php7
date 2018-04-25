FROM php:7.1-fpm-alpine

RUN apk add --update \
        icu-dev \
        zlib-dev \
        nodejs \
    && apk add --no-cache $PHPIZE_DEPS \
    && pecl install \
        xdebug \
        apcu \
    && docker-php-ext-install \
        opcache \
        intl \
		pdo_mysql \
        zip \
    && docker-php-ext-enable \
        xdebug \
        apcu \
        opcache

RUN rm -rf /var/cache/apk/* \
    && rm -rf /tmp/*

# composer
ENV COMPOSER_ALLOW_SUPERUSER 1
RUN curl --insecure https://getcomposer.org/composer.phar -o /usr/bin/composer \
    && chmod +x /usr/bin/composer
RUN composer self-update
RUN composer global require "hirak/prestissimo:^0.3" --prefer-dist --no-progress --no-suggest --optimize-autoloader --classmap-authoritative  --no-interaction

# php-cs-fixer
RUN curl -L http://cs.sensiolabs.org/download/php-cs-fixer-v2.phar -o /usr/bin/php-cs-fixer \
    && chmod +x /usr/bin/php-cs-fixer
RUN php-cs-fixer self-update

# mjml
#RUN npm install -g mjml