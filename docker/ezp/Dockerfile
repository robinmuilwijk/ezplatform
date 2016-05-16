FROM galileo/php:5.6-apache-advanced

# install xdebug
RUN yes | pecl install xdebug

WORKDIR /var/www/html

# Create ez platform virtual host
COPY bin/vhost.sh bin/vhost.sh
COPY doc/apache2/vhost.template doc/apache2/vhost.template
COPY docker/ezp/php.ini /usr/local/etc/php/conf.d/ez-php.ini
RUN bin/vhost.sh --basedir=/var/www/html \
      --template-file=doc/apache2/vhost.template \
      --host-name=local-ez.ez.no \
      | tee /etc/apache2/sites-available/000-default.conf > /dev/null

RUN a2ensite 000-default
RUN a2enmod rewrite

EXPOSE 80
