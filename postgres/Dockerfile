ARG POSTGRESQL_VERSION=latest
FROM postgres:${POSTGRESQL_VERSION}

MAINTAINER Leo Qin

# update timezone
ARG TIMEZONE=Asia/Shanghai
RUN /bin/cp /usr/share/zoneinfo/${TIMEZONE} /etc/localtime \
    && echo "${TIMEZONE}" > /etc/timezone;

CMD ["postgres"]

EXPOSE 5432
