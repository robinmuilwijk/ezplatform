FROM php:5.6-apache

RUN docker-php-ext-install exif
RUN docker-php-ext-install pdo pdo_mysql

RUN apt-get update && apt-get install -y libpng12-dev php5-curl php5-xsl php5-json php5-mcrypt php5-readline
RUN docker-php-ext-install mysqli
RUN apt-get install -y libxslt1-dev
RUN docker-php-ext-install xsl

# install intl
RUN apt-get update && apt-get install -y \
        libicu-dev \
    && docker-php-ext-install -j$(nproc) intl

# install gd
RUN apt-get update && apt-get install -y \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libpng12-dev \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install -j$(nproc) gd

# install xdebug
RUN yes | pecl install xdebug

WORKDIR /var/www/html

COPY bin/vhost.sh bin/vhost.sh
COPY doc/apache2/vhost.template doc/apache2/vhost.template
COPY docker/ezp/php.ini /usr/local/etc/php/conf.d/ez-php.ini

RUN bin/vhost.sh --basedir=/var/www/html \
      --template-file=doc/apache2/vhost.template \
      --host-name=local-ez.ez.no \
      | tee /etc/apache2/sites-available/000-default.conf > /dev/null

RUN a2ensite 000-default
RUN a2enmod rewrite

RUN apt-get update && apt-get install -y git

# Install composer
RUN curl -sS https://getcomposer.org/installer | php
RUN mv composer.phar /usr/local/bin/composer

EXPOSE 80
