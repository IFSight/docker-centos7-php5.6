FROM fulcrum/php:7-latest
MAINTAINER IF Fulcrum "fulcrum@ifsight.net"

# https://github.com/tideways
RUN   apk update \
   && apk add --virtual .build-deps git autoconf dpkg-dev dpkg file g++ gcc libc-dev make pkgconf re2c ca-certificates curl tar xz php7-dev \
   && cd /tmp/ \
   && git clone https://github.com/tideways/php-xhprof-extension.git \
   && cd php-xhprof-extension/ \
   && phpize \
   && ./configure \
   && make \
   && make install \
   && echo "extension=tideways_xhprof.so" > /etc/php7/conf.d/99_tidewater.ini \
   && apk del .build-deps && rm -rf tmp/* \
   && date
