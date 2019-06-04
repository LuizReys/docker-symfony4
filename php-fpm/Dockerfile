FROM php:7.3.6-fpm
 
MAINTAINER Luiz Reis <dluiz.reis@pravaler.com.br>

# Additional tools
RUN apt-get update \
 && apt-get install -y --no-install-recommends \
    curl \
    openssl \
    nano

# Common php-ext and requirements
RUN apt-get install -y --no-install-recommends libpq-dev libz-dev \
 && docker-php-ext-install pcntl \
 && docker-php-ext-install session \
 && docker-php-ext-install phar \
 && docker-php-ext-install iconv \
 && docker-php-ext-install pdo

#####################################
# PDO_POSTGRESQL:
#####################################

ARG INSTALL_PDO_POSTGRESQL=true
RUN if [ ${INSTALL_PDO_POSTGRESQL} = true ]; then \
    # Install pdo_pgsql
    docker-php-ext-install pdo_pgsql \
;fi

#####################################
# xdebug:
#####################################

ARG INSTALL_XDEBUG=true
RUN if [ ${INSTALL_XDEBUG} = true ]; then \
    # Install the xdebug
    pecl install xdebug \
    docker-php-ext-enable xdebug \
;fi

# Copy xdebug configration
COPY ./xdebug.ini /usr/local/etc/php/conf.d/xdebug.ini

#####################################
# composer:
#####################################

ARG INSTALL_COMPOSER=true
RUN if [ ${INSTALL_COMPOSER} = true ]; then \
    # Install the composer
    curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer \
;fi

# Copy xdebug configration
COPY ./xdebug.ini /usr/local/etc/php/conf.d/xdebug.ini

#####################################
# json, xml, dom xmlrpc, xsl:
#####################################

ARG INSTALL_JSON_XML=true
RUN if [ ${INSTALL_JSON_XML} = true ]; then \
    # Install xml, dom xmlrpc, xsl, and requirements
    apt-get install -y --no-install-recommends libxml2-dev libxslt-dev \
 && docker-php-ext-install json \
    xml \
    dom \
    xmlrpc \
    xsl \
;fi

#####################################
# curl:
#####################################

ARG INSTALL_CURL=true
RUN if [ ${INSTALL_CURL} = true ]; then \
   # Install curl and requirements
   apt-get install -y --no-install-recommends libcurl3 libcurl3-dev \
   docker-php-ext-install curl \
;fi

#####################################
# Human Language and Character Encoding Support:
#####################################

ARG INSTALL_INTL=false
RUN if [ ${INSTALL_INTL} = true ]; then \
    # Install intl and requirements
    apt-get install -y --no-install-recommends zlib1g-dev libicu-dev g++ \
 && docker-php-ext-configure intl \
 && docker-php-ext-install intl \
;fi

# Clear package lists
RUN rm -rf /var/lib/apt/lists/*

# Permissions
RUN chown -R root:www-data /var/www/html
RUN chmod u+rwx,g+rx,o+rx /var/www/html
RUN find /var/www/html -type d -exec chmod u+rwx,g+rx,o+rx {} +
RUN find /var/www/html -type f -exec chmod u+rw,g+rw,o+r {} +

CMD ["php-fpm"]

EXPOSE 9000