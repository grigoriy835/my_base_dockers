FROM debian:jessie-slim

RUN apt-get update
RUN apt-get install -y vim netcat mc git htop curl logrotate wget xterm

RUN apt-get install -y build-essential libpcre3 libpcre3-dev libcurl4-openssl-dev gcc libpcrecpp0 libssl-dev zlib1g-dev

COPY nginx-1.12.1 /nginx
WORKDIR /nginx
COPY nginx-sla-master nginx-sla-master

RUN ./configure --add-module=nginx-sla-master --with-http_ssl_module
run make install

WORKDIR /usr/local/nginx
RUN rm -Rf /nginx
COPY http_config /http_config

RUN ln -sf /dev/stdout /usr/local/nginx/logs/access.log \
    && ln -sf /dev/stderr /usr/local/nginx/logs/error.log

EXPOSE 80
EXPOSE 443
CMD ["/usr/local/nginx/sbin/nginx", "-g", "daemon off;"]
