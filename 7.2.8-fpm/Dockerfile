FROM php:7.2.8-fpm

COPY sources.list /etc/apt/sources.list
     
RUN apt-get update 

RUN apt-get install unzip zip

RUN apt-get install -y \
    libfreetype6-dev \
    libjpeg62-turbo-dev \
    libmcrypt-dev \
    libpng-dev\
    libmemcached-dev\
    libxml2-dev

RUN docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ 
RUN docker-php-ext-install -j$(nproc) zip gd mbstring mysqli pdo_mysql shmop soap

#install composer
RUN curl -sS https://getcomposer.org/installer | php
RUN mv composer.phar /usr/bin/composer
RUN chmod 777 /usr/bin/composer
RUN composer config -g repo.packagist composer https://packagist.phpcomposer.com

EXPOSE 9000

CMD ["php-fpm"]