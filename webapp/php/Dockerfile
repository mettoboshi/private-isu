FROM php:7.4-fpm

RUN apt update && apt install -y \
  unzip libmemcached-dev zlib1g-dev

RUN docker-php-ext-install pdo pdo_mysql

RUN apt-get install -y vim
RUN pecl install memcached \
  && docker-php-ext-enable memcached

RUN curl -sS https://getcomposer.org/installer | php \
  && mv composer.phar /usr/local/bin/composer

# RUN cp /usr/local/etc/php/php.ini-production /usr/local/etc/php/php.ini
RUN cp /usr/local/etc/php/php.ini-development /usr/local/etc/php/php.ini
COPY ./composer.json /var/www/html
COPY ./composer.lock /var/www/html
COPY ./php.ini /usr/local/etc/php/conf.d/php.ini

WORKDIR /var/www/html

RUN composer install --no-dev

COPY . /var/www/html
