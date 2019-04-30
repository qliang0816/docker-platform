FROM tomcat:latest

LABEL maintainer="Leo Qin"

# update timezone
ARG TZ=UTC
ENV TZ ${TZ}
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

# default expose
EXPOSE 8080

# default Tomcat server
CMD ["catalina.sh", "run"]
