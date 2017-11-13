FROM debian:jessie-slim

#install php
RUN apt-get update && apt-get install -y apt-transport-https\
    ca-certificates lsb-release wget vim mc git htop logrotate xterm

RUN wget -O /etc/apt/trusted.gpg.d/php.gpg https://packages.sury.org/php/apt.gpg
RUN echo "deb https://packages.sury.org/php/ $(lsb_release -sc) main" > /etc/apt/sources.list.d/php.list

RUN apt-get update && apt-get install -y php7.1\
    php7.1-cgi\
    php7.1-cli\
    php7.1-common\
    php7.1-curl\
    php7.1-fpm\
    php7.1-gd\
    php7.1-json\
    php7.1-mbstring\
    php7.1-mysql\
    php7.1-pgsql\
    php-xml\
    php-xdebug\
    php7.1-mcrypt\
    php-redis

#setup fpm
RUN sed -i "s/display_errors = Off/display_errors = stderr/" /etc/php/7.1/fpm/php.ini && \
    sed -i -e "s/;daemonize\s*=\s*yes/daemonize = no/g" /etc/php/7.1/fpm/php-fpm.conf && \
#    sed -i '/^listen = /clisten = 9000' /etc/php/7.1/fpm/pool.d/www.conf && \ # for port
    echo 'kek'

#turn off xdebug (for prod)
RUN mv /etc/php/7.1/mods-available/xdebug.ini /etc/php/7.1/mods-available/xdebug

EXPOSE 9000

RUN mkdir /run/php
ENTRYPOINT ["/usr/sbin/php-fpm7.1", "-F"]