ARG PHP_VERSION=7.2
FROM php:${PHP_VERSION}-fpm

LABEL maintainer="Leo Qin"

RUN apt-get update \
	&& apt-get install -y --no-install-recommends \
	curl \
	libmemcached-dev \
	libz-dev \
	libpq-dev \
	libjpeg-dev \
	libpng-dev \
	libfreetype6-dev \
	libssl-dev \
	libmcrypt-dev \
	&& rm -rf /var/lib/apt/lists/*

# Install the PHP pdo_mysql extention
RUN docker-php-ext-install pdo_mysql \
	# Install the PHP pdo_pgsql extention
	&& docker-php-ext-install pdo_pgsql \
	# Install the PHP gd library
	&& docker-php-ext-configure gd \
	--enable-gd-native-ttf \
	--with-jpeg-dir=/usr/lib \
	--with-freetype-dir=/usr/include/freetype2 && \
	docker-php-ext-install gd

# update timezone
ARG TZ=UTC
ENV TZ ${TZ}
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

WORKDIR /var/www

EXPOSE 9000
CMD ["php-fpm"]