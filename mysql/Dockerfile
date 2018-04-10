ARG MYSQL_VERSION=latest
FROM mysql:${MYSQL_VERSION}

MAINTAINER Leo Qin

# update timezone
ARG TIMEZONE=Asia/Shanghai
RUN ln -snf /usr/share/zoneinfo/${TIMEZONE} /etc/localtime \
    && echo "${TIMEZONE}" > /etc/timezone;

RUN chown -R mysql:root /var/lib/mysql/

ADD my.cnf /etc/mysql/conf.d/my.cnf

CMD ["mysqld"]

EXPOSE 3306
