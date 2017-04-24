FROM debian:stretch-slim

MAINTAINER bibaijin

ENV NGINX_VERSION 1.12.0

RUN apt-get update
RUN apt-get install -y wget
RUN apt-get install -y gcc
RUN apt-get install -y g++
RUN apt-get install -y make

WORKDIR /app

RUN wget ftp://ftp.csx.cam.ac.uk/pub/software/programming/pcre/pcre-8.40.tar.gz
RUN tar -zxf pcre-8.40.tar.gz
RUN cd pcre-8.40/ && ./configure && make && make install

RUN wget http://zlib.net/zlib-1.2.11.tar.gz
RUN tar -zxf zlib-1.2.11.tar.gz
RUN cd zlib-1.2.11/ && ./configure && make && make install

RUN wget http://www.openssl.org/source/openssl-1.0.2f.tar.gz
RUN tar -zxf openssl-1.0.2f.tar.gz
RUN ls -alh
RUN cat openssl-1.0.2f/Configure
RUN cd openssl-1.0.2f/ && ./config --prefix=/usr && make && make install

RUN wget http://nginx.org/download/nginx-${NGINX_VERSION}.tar.gz -O nginx-${NGINX_VERSION}.tar.gz
RUN tar -xzf nginx-${NGINX_VERSION}.tar.gz
RUN cd nginx-${NGINX_VERSION} \
    && ./configure --sbin-path=/usr/local/nginx/nginx \
                   --conf-path=/usr/local/nginx/nginx.conf \
                   --pid-path=/usr/local/nginx/nginx.pid \
                   --with-pcre=../pcre-8.40 \
                   --with-zlib=../zlib-1.2.11 \
                   --with-http_ssl_module \
                   --with-stream \
                   --with-mail=dynamic \
    && make && make install

RUN ln -s /usr/local/nginx/nginx /nginx

EXPOSE 80

STOPSIGNAL SIGQUIT

CMD ["/nginx", "-g", "daemon off;"]