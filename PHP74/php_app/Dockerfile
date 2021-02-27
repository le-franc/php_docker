FROM php:7.4-fpm
 
RUN apt-get update \
&& apt-get -y install \
libicu-dev \
libonig-dev \
gnupg

RUN DEBIAN_FRONTEND="noninteractive" apt-get -y install tzdata
 
RUN docker-php-ext-install intl

RUN docker-php-ext-install pcntl

#RUN docker-php-ext-install pdo_mysql
#RUN docker-php-ext-install mbstring

ENV ACCEPT_EULA=Y

# Microsoft SQL Server Prerequisites
RUN apt-get update \
    && curl https://packages.microsoft.com/keys/microsoft.asc | apt-key add - \
    && curl https://packages.microsoft.com/config/debian/9/prod.list \
        > /etc/apt/sources.list.d/mssql-release.list \
    && apt-get install -y --no-install-recommends \
        locales \
        apt-transport-https \
    && echo "en_US.UTF-8 UTF-8" > /etc/locale.gen \
    && locale-gen \
    && apt-get update \
    && apt-get -y --no-install-recommends install \
        unixodbc-dev \
        msodbcsql17

RUN docker-php-ext-install mbstring pdo pdo_mysql \
    && pecl install sqlsrv pdo_sqlsrv xdebug \
    && docker-php-ext-enable sqlsrv pdo_sqlsrv xdebug
 
RUN rm -rf /var/cache/apk/*
 
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/bin --filename=composer
 
CMD ["php-fpm"]