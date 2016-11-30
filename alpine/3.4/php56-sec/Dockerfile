FROM fulcrum/alpine
MAINTAINER IF Fulcrum "fulcrum@ifsight.net"

# PHP security updates have had excessive lag time as available Alpine packages
# Due to this the PHP packages are created from the
# fulcrum/alpine-sdk-php conainer and used here.
ADD packages /root/packages/

RUN apk update && apk upgrade && \
    cd /root/packages && \
    apk add --allow-untrusted php5-*-r0.apk postfix && \
    adduser -h /var/www/html -s /sbin/nologin -D -H -u 1971 php && \
    chown -R postfix  /var/spool/postfix                        && \
    chgrp -R postdrop /var/spool/postfix/public                 && \
    chgrp -R postdrop /var/spool/postfix/maildrop               && \
    chown -R root     /var/spool/postfix/pid                    && \
    chown    root     /var/spool/postfix                        && \
    echo smtputf8_enable = no >> /etc/postfix/main.cf           && \
    rm -rf /root/packages

ENTRYPOINT ["/usr/bin/php-fpm"]

CMD ["--nodaemonize"]
