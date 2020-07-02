FROM nginx:alpine

LABEL maintainer="Leo Qin"

# update timezone
ARG TZ=UTC
ENV TZ ${TZ}

COPY nginx.conf /etc/nginx/

RUN sed -i 's/dl-cdn.alpinelinux.org/mirrors.aliyun.com/g' /etc/apk/repositories

RUN apk update \
    && apk upgrade \
    && apk add --no-cache bash \
    && rm /etc/nginx/conf.d/default.conf \
    && ln -snf /usr/share/zoneinfo/$TZ /etc/localtime \
    && echo $TZ > /etc/timezone

CMD ["nginx"]

EXPOSE 80 443
