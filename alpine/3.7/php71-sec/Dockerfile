FROM alpine:3.7
MAINTAINER IF Fulcrum "fulcrum@ifsight.net"

# PHP security updates have had excessive lag time as available Alpine packages
# Due to this the PHP packages are created from the
# fulcrum/alpine-sdk-php conainer and used here.
ADD packages /root/packages/

RUN apk update && apk upgrade && \
    cd /root/packages && \
    apk add --allow-untrusted php7-*-r0.apk postfix && \
    adduser -h /var/www/html -s /sbin/nologin -D -H -u 1971 php && \
    chown -R postfix  /var/spool/postfix                        && \
    chgrp -R postdrop /var/spool/postfix/public                 && \
    chgrp -R postdrop /var/spool/postfix/maildrop               && \
    chown -R root     /var/spool/postfix/pid                    && \
    chown    root     /var/spool/postfix                        && \
    echo smtputf8_enable = no >> /etc/postfix/main.cf           && \
    rm -rf /root/packages \
    && apk add curl \
    && version=$(php -r "echo PHP_MAJOR_VERSION.PHP_MINOR_VERSION;") \
    && curl -A "Docker" -o /blackfire-probe.tar.gz -D - -L -s https://blackfire.io/api/v1/releases/probe/php/alpine/amd64/$version \
    && tar zxpf /blackfire-probe.tar.gz -C / \
    && mv /blackfire-*.so $(php -r "echo ini_get('extension_dir');")/blackfire.so \
    && printf "extension=blackfire.so\nblackfire.agent_socket=tcp://blackfire:8707\n" > /etc/php7/conf.d/90-blackfire.ini \
    && apk del curl \
    && rm /blackfire*

ENTRYPOINT ["/usr/bin/php-fpm"]

CMD ["--nodaemonize"]
