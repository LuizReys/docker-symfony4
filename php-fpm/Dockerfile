FROM php:7.2-fpm
 
MAINTAINER Luiz Reis <luiz.reis@pravaler.com.br>

RUN apt-get clean
RUN apt-get update

#####################################
# Libs:
#####################################
RUN echo 'deb http://httpredir.debian.org/debian jessie contrib' >> /etc/apt/sources.list

RUN export DEBIAN_FRONTEND=noninteractive && apt-get install -y --force-yes libssl-dev curl  libcurl4-gnutls-dev libxml2-dev libicu-dev libmcrypt4 libmemcached11 openssl

RUN apt-get install -y zlib1g-dev libpq-dev git curl vim libicu-dev libxml2-dev \
    && docker-php-ext-configure intl \
    && docker-php-ext-install intl \
    && docker-php-ext-configure pgsql -with-pgsql=/usr/local/pgsql \
    && docker-php-ext-install pdo pdo_pgsql pgsql \
&& docker-php-ext-install zip xml

#####################################
# Composer:
#####################################
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

#####################################
# Clear package lists:
#####################################
RUN rm -rf /var/lib/apt/lists/*

#####################################
# Permissions:
#####################################
RUN chown -R root:www-data /var/www/html
RUN chmod u+rwx,g+rx,o+rx /var/www/html
RUN find /var/www/html -type d -exec chmod u+rwx,g+rx,o+rx {} +
RUN find /var/www/html -type f -exec chmod u+rw,g+rw,o+r {} +

CMD ["php-fpm"]

EXPOSE 9000