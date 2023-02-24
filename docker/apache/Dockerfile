FROM php:8.2-apache
#RUN curl -OL https://github.com/composer/composer/releases/download/2.0.11/composer.phar
#RUN mv composer.phar /usr/local/bin/composer
#RUN chmod +x /usr/local/bin/composer && a2enmod rewrite && service apache2 restart
RUN apt-get update && apt-get install -y nano
RUN apt-get install -y  git
# renseignez votre mail
RUN git config --global user.email "<YOUR_MAIL>"
# renseignez votre nom de user
RUN git config --global user.name "<YOUR_NAME>"
#RUN apt-get install -y wget
#RUN wget https://get.symfony.com/cli/installer -O - | bash
#RUN mv /root/.symfony/bin/symfony /usr/local/bin/symfony
RUN docker-php-ext-install pdo_mysql
#RUN apt-get install -y zip
#RUN apt-get install -y zlib1g-dev libicu-dev g++
#RUN docker-php-ext-configure intl
#RUN docker-php-ext-install intl

#RUN openssl req -new -newkey rsa:4096 -days 3650 -nodes -x509 -subj \
#"/C=nc/ST=fr/L=pe/O=nc/CN=toto.fr" \
#-keyout ./ssl.key -out ./ssl.crt

#RUN mkdir /etc/apache2/ssl
#RUN cp ./ssl.crt /etc/apache2/ssl/ssl.crt
#RUN cp  ./ssl.key /etc/apache2/ssl/ssl.key

RUN mkdir -p /var/run/apache2/
#RUN a2enmod ssl
#EXPOSE 80
#EXPOSE 443


#XDEBUG
WORKDIR /var/www/html/

RUN pecl install xdebug \
    && docker-php-ext-enable xdebug \
    && echo "zend_extension=$(find /usr/local/lib/php/extensions/ -name xdebug.so)" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini \
    && echo "xdebug.mode=debug,profile" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini \
    && echo "xdebug.start_with_request=yes" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini \
    && echo "xdebug.client_host=host.docker.internal" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini \
    && echo "xdebug.client_port=9003" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini \

RUN echo "zend_extension=$(find /usr/local/lib/php/extensions/ -name xdebug.so)" >> /usr/local/etc/php/php.ini-development \
    && echo "xdebug.mode=debug,profile" >> /usr/local/etc/php/php.ini-development \
    && echo "xdebug.start_with_request=yes" >> /usr/local/etc/php/php.ini-development \
    && echo "xdebug.client_host=host.docker.internal" >> /usr/local/etc/php/php.ini-development \
    && echo "xdebug.client_port=9003" >> /usr/local/etc/php/php.ini-development \

#Create phpinfo
RUN echo "<?php phpinfo(); ?>" >> /var/www/html/phpinfo.php