ARG PHP_VERSION=72
FROM leoqin/php${PHP_VERSION}-fpm-base

LABEL maintainer="Leo Qin"

# update timezone
ARG TZ=UTC
ENV TZ ${TZ}
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

WORKDIR /var/www

EXPOSE 9000
CMD ["php-fpm"]