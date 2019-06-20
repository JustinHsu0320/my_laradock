ARG PHP_VERSION
FROM php:${PHP_VERSION}-apache

RUN apt-get -y update --fix-missing
RUN apt-get upgrade -y

# Install cron & editor
RUN apt-get install -y cron vim

# Install useful tools
RUN apt-get -y install apt-utils nano wget dialog

# Install important libraries
RUN apt-get -y install --fix-missing apt-utils build-essential git curl libcurl3 libcurl3-dev zip openssl

# Composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

# Install xdebug
RUN pecl install xdebug-2.6.0
RUN docker-php-ext-enable xdebug

# Install redis
RUN pecl install redis-4.0.1
RUN docker-php-ext-enable redis

# Other PHP7 Extensions

RUN apt-get -y install libsqlite3-dev libsqlite3-0 mysql-client
RUN docker-php-ext-install pdo_mysql
RUN docker-php-ext-install pdo_sqlite
RUN docker-php-ext-install mysqli

RUN docker-php-ext-install curl
RUN docker-php-ext-install tokenizer
RUN docker-php-ext-install json

RUN apt-get -y install zlib1g-dev
RUN docker-php-ext-install zip

RUN apt-get -y install libicu-dev
RUN docker-php-ext-install -j$(nproc) intl

RUN docker-php-ext-install mbstring
RUN docker-php-ext-install gettext

RUN apt-get install -y libfreetype6-dev libjpeg62-turbo-dev libpng-dev
RUN docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/
RUN docker-php-ext-install -j$(nproc) gd

RUN apt-get install -y net-tools

RUN apt-get install -y ntp

RUN apt-get install -y supervisor

#
#--------------------------------------------------------------------------
# Optional Supervisord Configuration
#--------------------------------------------------------------------------
#
# Modify the ./supervisor.conf file to match your App's requirements.
# Make sure you rebuild your container with every change.
#

COPY supervisord.conf /etc/supervisor/supervisord.conf

ENTRYPOINT ["/usr/bin/supervisord", "-n", "-c",  "/etc/supervisor/supervisord.conf"]

# 網路校正時間指令
# sudo ntpdate watch.stdtime.gov.tw

# 設置時區
RUN /bin/cp /usr/share/zoneinfo/Asia/Taipei /etc/localtime \
    && echo 'Asia/Taipei' >/etc/timezone

# Enable apache modules
RUN a2enmod rewrite headers ssl

COPY vhost.conf /etc/apache2/sites-enabled/vhost.conf

EXPOSE 80
