FROM php:7.2-fpm


RUN apt-get update && apt-get install -y \
	gnupg \
	git \
	zlib1g-dev \
	zip \
	unzip \
	curl \
	ca-certificates \
	libmcrypt-dev \
	openssl \
	apt-transport-https 

RUN curl https://www.postgresql.org/media/keys/ACCC4CF8.asc | apt-key add -
RUN sh -c 'echo "deb http://apt.postgresql.org/pub/repos/apt/ stretch-pgdg main" > /etc/apt/sources.list.d/pgdg.list'
RUN apt-get update && apt-get -y install postgresql-11 postgresql-server-dev-11

#RUN curl https://www.postgresql.org/media/keys/ACCC4CF8.asc | apt-key add -
#RUN sh -c 'echo "deb http://apt.postgresql.org/pub/repos/apt/ stretch-pgdg main" > /etc/apt/sources.list.d/pgdg.list'

# Need this as a pre-requisite for pdo_pgsql
#RUN set -ex && apk --no-cache add postgresql-dev

RUN pecl install mcrypt-1.0.2
RUN docker-php-ext-enable mcrypt

RUN docker-php-ext-install \
	pdo \
	pdo_pgsql \
	mbstring \
	zip

RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer
ADD . /var/www/

RUN usermod -u 1000 www-data
RUN chown -R www-data:www-data .
USER www-data

WORKDIR /var/www/
#RUN composer install --prefer-dist