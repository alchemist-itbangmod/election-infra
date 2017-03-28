FROM alpine:edge

RUN echo "http://dl-4.alpinelinux.org/alpine/edge/testing" >> /etc/apk/repositories

RUN apk update && \
    apk add nginx bash ca-certificates s6 curl ssmtp php7 php7-phar php7-curl \
    php7-fpm php7-json php7-zlib php7-xml php7-dom php7-ctype php7-opcache php7-zip php7-iconv \
    php7-pdo php7-pdo_mysql php7-pdo_sqlite php7-pdo_pgsql php7-mbstring php7-session \
    php7-gd php7-mcrypt php7-openssl php7-sockets php7-posix php7-ldap php7-timezonedb && \
    rm -rf /var/cache/apk/* && \
    ln -sfn /usr/bin/php7 /usr/bin/php && \
    rm -f /etc/php7/php-fpm.d/www.conf && \
    touch /etc/php7/php-fpm.d/env.conf

RUN curl -sS https://getcomposer.org/installer | php -- --filename=/usr/local/bin/composer

RUN rm -rf /var/www/* && mkdir /var/www/app

COPY ./config/php/conf.d/local.ini /etc/php7/conf.d/
COPY ./config/php/php-fpm.conf /etc/php7/
COPY ./config/nginx/nginx.conf /etc/nginx/nginx.conf
COPY ./config/services.d /etc/services.d

EXPOSE 80

ENTRYPOINT ["/bin/s6-svscan", "/etc/services.d"]
CMD []