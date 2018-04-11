ARG MYSQL_VERSION=latest
FROM mysql:${MYSQL_VERSION}

MAINTAINER Leo Qin

# update timezone
ARG TZ=PRC
RUN ln -snf /usr/share/zoneinfo/${TZ} /etc/localtime \
    && echo "${TZ}" > /etc/timezone \
    && TZ="${TZ}"; export TZ

RUN chown -R mysql:root /var/lib/mysql/

ADD my.cnf /etc/mysql/conf.d/my.cnf

CMD ["mysqld"]

EXPOSE 3306
