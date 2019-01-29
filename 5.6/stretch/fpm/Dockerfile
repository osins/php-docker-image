FROM php:5.6-fpm

COPY sources.163.list /etc/apt/sources.list
RUN DEBIAN_FRONTEND=noninteractive apt-get update -q
RUN DEBIAN_FRONTEND=noninteractive apt-get dist-upgrade -y 
RUN DEBIAN_FRONTEND=noninteractive apt-get install -y \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libmcrypt-dev \
        libpng-dev \
        libcurl4-nss-dev \
        libmemcached-dev 
RUN pecl install redis-4.0.1
RUN pecl install memcached-2.2.0
RUN docker-php-ext-install iconv mcrypt
RUN docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/
RUN docker-php-ext-install gd
RUN docker-php-ext-install curl
RUN docker-php-ext-install mysqli
RUN docker-php-ext-install pdo
RUN docker-php-ext-install pdo_mysql
RUN docker-php-ext-install mbstring
RUN docker-php-ext-install json 
RUN docker-php-ext-enable memcached
RUN docker-php-ext-enable redis

RUN apt-get install -y git wget nano unzip inetutils-ping 
RUN wget https://getcomposer.org/download/1.8.0/composer.phar && mv composer.phar /usr/local/bin/composer && chmod -R 777 /usr/local/bin/composer 
RUN composer config -g repo.packagist composer https://packagist.phpcomposer.com

CMD ["/usr/local/sbin/php-fpm", "--nodaemonize"]