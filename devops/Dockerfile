# https://github.com/docker-library/php/blob/bb80b576dd6da2fd73760f5dd3a3a89980805703/7.3/buster/fpm/Dockerfile
FROM php:7.4-fpm
ARG MYSQL_PORT

RUN apt-get update \
        && apt-get -y install wait-for-it git zip default-mysql-client iputils-ping

# Install php extensions
RUN docker-php-ext-install pdo_mysql

RUN wait-for-it 172.17.0.1:$MYSQL_PORT
RUN mysql -h 172.17.0.1 --port $MYSQL_PORT -u root -p=root

RUN ping 172.17.0.1 -c 4

# Change the user to www-data
USER www-data
# On container start-up run the following entry script.
CMD ["/usr/bin/entry-scripts/startup.sh"]
