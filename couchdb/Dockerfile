FROM apache/couchdb:latest

LABEL maintainer="Leo Qin"

# update timezone
ARG TZ=UTC
ENV TZ ${TZ}
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

# Add configuration
COPY local.ini /opt/couchdb/etc/

EXPOSE 5984
