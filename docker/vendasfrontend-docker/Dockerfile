FROM php:7-apache

MAINTAINER  Hugo Pereira <hugopereira84@gmail.com>

RUN apt-get update && apt-get install -y \
        libmcrypt-dev \
        git \
        zlib1g-dev \
        libldap2-dev \
        && apt-get clean \
        && rm -rf /var/lib/apt/lists/* \
        && docker-php-ext-configure ldap --with-libdir=lib/x86_64-linux-gnu/ \
        && docker-php-ext-install ldap

# Basic lumen packages
RUN docker-php-ext-install \
        mcrypt \
        mbstring \
        tokenizer \
        zip

# Enable apache mods.
RUN /usr/sbin/a2enmod rewrite

# Update the default apache site with the config we created.
ADD ./apache.vhost.conf /etc/apache2/sites-enabled/000-default.conf

# By default start up apache in the foreground, override with /bin/bash for interative.
CMD /usr/sbin/apache2ctl -D FOREGROUND

# Install composer
RUN curl -sS https://getcomposer.org/installer | \
    php -- --install-dir=/usr/bin/ --filename=composer


# fix permissions
#ARG APP_USER=www
#RUN useradd --user-group --create-home --shell /bin/false ${APP_USER}
#USER ${APP_USER}

#Fix 
#WORKDIR /var/www/frontend
#CMD /usr/local/bin/php artisan key:generate
#RUN /usr/local/bin/php artisan key:generate

# Expose apache.
EXPOSE 80




