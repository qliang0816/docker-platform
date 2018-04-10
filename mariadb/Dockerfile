ARG MARIADB_VERSION=latest
FROM mariadb:${MARIADB_VERSION}

MAINTAINER Leo Qin

# update timezone
ARG TIMEZONE=Asia/Shanghai
RUN /bin/cp /usr/share/zoneinfo/${TIMEZONE} /etc/localtime \
    && echo "${TIMEZONE}" > /etc/timezone;

ADD my.cnf /etc/mysql/conf.d/my.cnf

CMD ["mysqld"]

EXPOSE 3306
