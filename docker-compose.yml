version: '3'

services:

### NODE Container #######################################

node:
    image: "node:9"
    user: "node"
    working_dir: /var/www
    environment:
      - NODE_ENV=${NODE_ENV}
    volumes:
      - ./:/var/www
    expose:
      - "8081"
    command: "npm start"

### PHP-FPM Container #######################################

    php-fpm:
      build:
        context: ./php-fpm
        dockerfile: "Dockerfile-${PHP_VERSION}"
      volumes:
        - ./php-fpm/php${PHP_VERSION}.ini:/usr/local/etc/php/php.ini
      expose:
        - "9000"
      networks:
        - backend

### couchdb Container #######################################
    couchdb:
      build:
        context: ./couchdb
      environment:
        - COUCHDB_USER=admin
        - COUCHDB_PASSWORD=admin
      volumes:
        - ${DATA_SAVE_PATH}/couchdb/:/opt/couchdb/data
        - ./couchdb/:/usr/local/etc/couchdb/
        - ./logs/couchdb/:/usr/local/var/log/couchdb/
      ports:
        - "5984:5984"
        - "4369:4369"
        - "9100:9100"
      depends_on:
        - php-fpm
      networks:
        - backend

### NGINX Server Container ##################################

    nginx:
      build:
        context: ./nginx
      volumes_from:
        - applications
      volumes:
        - ${NGINX_HOST_LOG_PATH}:/var/log/nginx
        - ${NGINX_SITES_PATH}:/etc/nginx/sites-available
      ports:
        - "${NGINX_HOST_HTTP_PORT}:80"
        - "${NGINX_HOST_HTTPS_PORT}:443"
      depends_on:
        - php-fpm
      networks:
        - frontend
        - backend

### Apache Server Container #################################

    apache2:
      build:
        context: ./apache2
        args:
          - PHP_UPSTREAM_CONTAINER=${APACHE_PHP_UPSTREAM_CONTAINER}
          - PHP_UPSTREAM_PORT=${APACHE_PHP_UPSTREAM_PORT}
          - PHP_UPSTREAM_TIMEOUT=${APACHE_PHP_UPSTREAM_TIMEOUT}
      volumes_from:
        - applications
      volumes:
        - ${APACHE_HOST_LOG_PATH}:/var/log/apache2
        - ${APACHE_SITES_PATH}:/etc/apache2/sites-available
      ports:
        - "${APACHE_HOST_HTTP_PORT}:80"
        - "${APACHE_HOST_HTTPS_PORT}:443"
      depends_on:
        - php-fpm
      networks:
        - frontend
        - backend

### MySQL Container #########################################

    mysql:
      build:
        context: ./mysql
        args:
          - MYSQL_VERSION=${MYSQL_VERSION}
      environment:
        - MYSQL_DATABASE=${MYSQL_DATABASE}
        - MYSQL_USER=${MYSQL_USER}
        - MYSQL_PASSWORD=${MYSQL_PASSWORD}
        - MYSQL_ROOT_PASSWORD=${MYSQL_ROOT_PASSWORD}
        - TZ=${WORKSPACE_TIMEZONE}
      volumes:
        - ${DATA_SAVE_PATH}/mysql:/var/lib/mysql
        - ${MYSQL_ENTRYPOINT_INITDB}:/docker-entrypoint-initdb.d
      ports:
        - "${MYSQL_PORT}:3306"
      networks:
        - backend

### MariaDB Container #######################################

    mariadb:
      build: ./mariadb
      volumes:
        - ${DATA_SAVE_PATH}/mariadb:/var/lib/mysql
        - ${MARIADB_ENTRYPOINT_INITDB}:/docker-entrypoint-initdb.d
      ports:
        - "${MARIADB_PORT}:3306"
      environment:
        - MYSQL_DATABASE=${MARIADB_DATABASE}
        - MYSQL_USER=${MARIADB_USER}
        - MYSQL_PASSWORD=${MARIADB_PASSWORD}
        - MYSQL_ROOT_PASSWORD=${MARIADB_ROOT_PASSWORD}
      networks:
        - backend

### PostgreSQL Container ####################################

    postgres:
      build: ./postgres
      volumes:
        - ${DATA_SAVE_PATH}/postgres:/var/lib/postgresql/data
      ports:
        - "${POSTGRES_PORT}:5432"
      environment:
        - POSTGRES_DB=${POSTGRES_DB}
        - POSTGRES_USER=${POSTGRES_USER}
        - POSTGRES_PASSWORD=${POSTGRES_PASSWORD}
      networks:
        - backend

### MongoDB Container #######################################

    mongo:
      build: ./mongo
      ports:
        - "${MONGODB_PORT}:27017"
      volumes:
        - ${DATA_SAVE_PATH}/mongo:/data/db
      networks:
        - backend

### Redis Container #########################################

    redis:
      build: ./redis
      volumes:
        - ${DATA_SAVE_PATH}/redis:/data
      ports:
        - "${REDIS_PORT}:6379"
      networks:
        - backend

### Memcached Container #####################################

    memcached:
      build: ./memcached
      volumes:
        - ${DATA_SAVE_PATH}/memcached:/var/lib/memcached
      ports:
        - "${MEMCACHED_HOST_PORT}:11211"
      depends_on:
        - php-fpm
      networks:
        - backend

### RabbitMQ Container ######################################

    rabbitmq:
      build: ./rabbitmq
      ports:
        - "${RABBITMQ_NODE_HOST_PORT}:5672"
        - "${RABBITMQ_MANAGEMENT_HTTP_HOST_PORT}:15672"
        - "${RABBITMQ_MANAGEMENT_HTTPS_HOST_PORT}:15671"
      privileged: true
      environment:
        - RABBITMQ_DEFAULT_USER=${RABBITMQ_DEFAULT_USER}
        - RABBITMQ_DEFAULT_PASS=${RABBITMQ_DEFAULT_PASS}
      depends_on:
        - php-fpm
      networks:
        - backend

### ElasticSearch Container #################################

    elasticsearch:
      build: ./elasticsearch
      volumes:
        - elasticsearch-data:/usr/share/elasticsearch/data
        - elasticsearch-plugins:/usr/share/elasticsearch/plugins
      environment:
        - cluster.name=laradock-cluster
        - bootstrap.memory_lock=true
        - "ES_JAVA_OPTS=-Xms256m -Xmx256m"
      ulimits:
        memlock:
          soft: -1
          hard: -1
      mem_limit: 512m
      ports:
        - "${ELASTICSEARCH_HOST_HTTP_PORT}:9200"
        - "${ELASTICSEARCH_HOST_TRANSPORT_PORT}:9300"
      depends_on:
        - php-fpm
      networks:
        - frontend
        - backend
### Networks Setup ############################################

networks:
  frontend:
    driver: "bridge"
  backend:
    driver: "bridge"

### Volumes Setup #############################################

volumes:
  mysql:
    driver: "local"
  postgres:
    driver: "local"
  memcached:
    driver: "local"
  redis:
    driver: "local"
  mariadb:
    driver: "local"
  mongo:
    driver: "local"
  elasticsearch-data:
    driver: "local"
  elasticsearch-plugins:
    driver: "local"
