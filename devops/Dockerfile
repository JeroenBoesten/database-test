# https://github.com/docker-library/php/blob/bb80b576dd6da2fd73760f5dd3a3a89980805703/7.3/buster/fpm/Dockerfile
FROM php:7.4-fpm

RUN apt-get update \
        && apt-get -y install wait-for-it git zip jpegoptim optipng pngquant gifsicle ffmpeg default-mysql-client libmcrypt-dev libonig-dev libmagickwand-dev\
        && apt-get -y install nano ##TEMP

# Install php extensions
RUN  pecl install mcrypt \
        && docker-php-ext-enable mcrypt \
        && pecl install redis \
        && docker-php-ext-enable redis \
        && docker-php-ext-install pdo_mysql \
        && docker-php-ext-install pcntl \
        && docker-php-ext-install mbstring \
        && docker-php-ext-configure gd --with-jpeg=/usr/lib --with-freetype=/usr/include/freetype2 \
        && docker-php-ext-install gd \
        && docker-php-ext-install json \
        && docker-php-ext-install fileinfo \
        && pecl install pcov \
        && docker-php-ext-enable pcov

RUN wait-for-it 172.17.0.1:3306
RUN mysql -h 172.17.0.1 --port 3306 -u root -p

# Change the user to www-data
USER www-data
# On container start-up run the following entry script.
CMD ["/usr/bin/entry-scripts/startup.sh"]
