FROM fulcrum/php:latest-alpine
MAINTAINER IF Fulcrum "fulcrum@ifsight.net"

ENV XDEBUG_VERSION 2.3.3

RUN    apk update && apk add --virtual .build-deps autoconf gcc ca-certificates openssl \
       g++ zlib-dev file libc-dev make pkgconf php5-dev \
    && update-ca-certificates \
    && cd /tmp && wget http://xdebug.org/files/xdebug-$XDEBUG_VERSION.tgz \
    && tar -zxvf xdebug-$XDEBUG_VERSION.tgz \
    && cd xdebug-$XDEBUG_VERSION && phpize \
    && ./configure --enable-xdebug && make && make install \
    && rm -rf /tmp/* \
    && rm -rf /var/cache/apk/* \
    && apk del .build-deps && rm -rf tmp/*

# docker volume mount this in /etc/php5/conf.d/xdebug.ini
#    zend_extension=/usr/lib/php5/modules/xdebug.so
#    xdebug.remote_enable=on
#    xdebug.remote_handler=dbgp
#    xdebug.remote_connect_back=1
#    xdebug.remote_autostart=on
#    xdebug.remote_port=9004
