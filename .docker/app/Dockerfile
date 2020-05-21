FROM php:7.3.6-fpm-alpine3.9

RUN apk update
RUN apk add --no-cache openssl bash mysql-client libzip-dev zip wget curl
RUN docker-php-ext-install pdo pdo_mysql zip bcmath
RUN docker-php-ext-configure zip

ENV DOCKERIZE_VERSION v0.6.1
RUN wget https://github.com/jwilder/dockerize/releases/download/$DOCKERIZE_VERSION/dockerize-linux-amd64-$DOCKERIZE_VERSION.tar.gz \
    && tar -C /usr/local/bin -xzvf dockerize-linux-amd64-$DOCKERIZE_VERSION.tar.gz \
    && rm dockerize-linux-amd64-$DOCKERIZE_VERSION.tar.gz

WORKDIR /var/www
RUN curl -s https://getcomposer.org/installer | php
RUN mv composer.phar /usr/local/bin/composer

RUN rm -rf /var/www/html
RUN ln -s public html

EXPOSE 9000
ENTRYPOINT ["php-fpm"]
