FROM rabbitmq:alpine

LABEL maintainer="Leo Qin"

# update timezone
ARG TZ=UTC
ENV TZ ${TZ}
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

RUN rabbitmq-plugins enable --offline rabbitmq_management

EXPOSE 4369 5671 5672 15671 15672 25672
