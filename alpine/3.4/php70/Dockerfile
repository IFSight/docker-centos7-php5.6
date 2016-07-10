FROM fulcrum/alpine
MAINTAINER IF Fulcrum "fulcrum@ifsight.net"

RUN echo '@testing http://dl-cdn.alpinelinux.org/alpine/edge/testing' >> /etc/apk/repositories && \
    apk update && apk upgrade && \
    apk add php7 php7-ctype php7-curl php7-dom php7-fpm php7-gd php7-gettext php7-imap php7-json php7-ldap php7-mcrypt php7-opcache php7-pdo php7-pdo_mysql php7-redis@testing php7-soap php7-sockets php7-xml php7-zip postfix && \
    adduser -h /var/www/html -s /sbin/nologin -D -H -u 1971 php

ENTRYPOINT ["/usr/bin/php-fpm"]

CMD ["--nodaemonize"]
