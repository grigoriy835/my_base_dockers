FROM debian:jessie-slim

RUN apt-get update && apt-get install -y apt-transport-https\
                      ca-certificates lsb-release wget vim mc git htop xterm

RUN wget -O /etc/apt/trusted.gpg.d/php.gpg https://packages.sury.org/php/apt.gpg
RUN echo "deb https://packages.sury.org/php/ $(lsb_release -sc) main" > /etc/apt/sources.list.d/php.list

RUN apt-get update && apt-get install -y\
    php5\
    php5-cli\
    php5-fpm\
    php5-cgi\
    php5-common\
    php5-curl\
    php5-fpm\
    php5-gd\
    php5-json\
    php5-mysql\
    php5-pgsql\
    php5-xdebug\
    php5-mcrypt\
    php5-redis\
    php-mbstring\
    php-xml

RUN sed -i "s/display_errors = Off/display_errors = stderr/" /etc/php5/fpm/php.ini && \
    sed -i -e "s/;daemonize\s*=\s*yes/daemonize = no/g" /etc/php5/fpm/php-fpm.conf && \
#    sed -i '/^listen = /clisten = 9000' /etc/php/7.1/fpm/pool.d/www.conf && \
    echo 'kek'

RUN mv /etc/php5/mods-available/xdebug.ini /etc/php5/mods-available/xdebug

ENTRYPOINT ["/usr/sbin/php5-fpm", "-F"]