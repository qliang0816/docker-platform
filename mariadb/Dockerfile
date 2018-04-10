ARG MARIADB_VERSION=latest
FROM mariadb:${MARIADB_VERSION}

MAINTAINER Leo Qin

# update timezone
ARG TZ=Asia/Shanghai
RUN ln -snf /usr/share/zoneinfo/${TZ} /etc/localtime \
    && echo "${TZ}" > /etc/timezone \
    && echo TZ="${TZ}"; export TZ

ADD my.cnf /etc/mysql/conf.d/my.cnf

CMD ["mysqld"]

EXPOSE 3306
