FROM php:5.6.36-fpm

RUN apt-get update \
&& apt-get -y install \
libicu-dev \
libonig-dev \
gnupg \
nano

RUN apt-get update ;\
apt-get install -y --no-install-recommends \
freetds-dev freetds-bin freetds-common libdbd-freetds libsybdb5 libqt4-sql-tds libqt5sql5-tds ;\
ln -s /usr/lib/x86_64-linux-gnu/libsybdb.so /usr/lib/libsybdb.so ;\
ln -s /usr/lib/x86_64-linux-gnu/libsybdb.a /usr/lib/libsybdb.a ;\
docker-php-ext-install mssql ;\
docker-php-ext-configure mssql

RUN docker-php-ext-install intl

RUN docker-php-ext-install pcntl

RUN rm -rf /var/cache/apk/*
 
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/bin --filename=composer

COPY php.ini /usr/local/etc/php/

RUN sed -ri -e 's!;date.timezone =!date.timezone = "America/Sao_Paulo"!g' /usr/local/etc/php/php.ini
RUN sed -ri -e 's!;default_charset =!default_charset = "iso-8859-1"!g' /usr/local/etc/php/php.ini

CMD ["php-fpm"]