FROM nginx:alpine

LABEL maintainer="Leo Qin"

ADD nginx.conf /etc/nginx/

RUN apk update \
    && apk upgrade \
    && apk add --no-cache bash \
    && adduser -D -H -u 1000 -s /bin/bash www-data
    && rm /etc/nginx/conf.d/default.conf

CMD ["nginx"]

EXPOSE 80 443
