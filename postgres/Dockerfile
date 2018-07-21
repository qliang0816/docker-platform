ARG POSTGRESQL_VERSION=latest
FROM postgres:${POSTGRESQL_VERSION}

MAINTAINER Leo Qin

# update timezone
ARG TZ=UTC
ENV TZ ${TZ}
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

CMD ["postgres"]

EXPOSE 5432
