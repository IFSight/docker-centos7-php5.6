FROM fulcrum/alpine
MAINTAINER IF Fulcrum "fulcrum@ifsight.net"






RUN echo 'http://dl-cdn.alpinelinux.org/alpine/edge/community' >> /etc/apk/repositories && \
    echo 'http://dl-cdn.alpinelinux.org/alpine/edge/testing'   >> /etc/apk/repositories && \
    echo 'http://dl-cdn.alpinelinux.org/alpine/edge/main'      >> /etc/apk/repositories && \
    apk update && apk upgrade && \
    apk add php7 php7-ctype php7-curl php7-dom php7-fpm php7-ftp php7-gd php7-gettext php7-imap php7-json php7-ldap php7-mbstring php7-mcrypt php7-mysqli php7-opcache php7-openssl php7-pdo php7-pdo_mysql php7-redis php7-soap php7-sockets php7-xml php7-zlib php7-zip postfix && \
    adduser -h /var/www/html -s /sbin/nologin -D -H -u 1971 php && \
    chown -R postfix  /var/spool/postfix                        && \
    chgrp -R postdrop /var/spool/postfix/public                 && \
    chgrp -R postdrop /var/spool/postfix/maildrop               && \
    chown -R root     /var/spool/postfix/pid                    && \
    chown    root     /var/spool/postfix                        && \
    echo smtputf8_enable = no >> /etc/postfix/main.cf


ENTRYPOINT ["/usr/sbin/php-fpm7"]

CMD ["--nodaemonize"]
