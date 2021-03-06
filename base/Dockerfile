FROM alpine:3.7
MAINTAINER Tommy Muehle <tommy.muehle@gmail.com>

ENV COMPOSER_HOME /composer
ENV COMPOSER_ALLOW_SUPERUSER 1
ENV PATH /composer/vendor/bin:$PATH

RUN apk --update --progress --no-cache --repository http://dl-cdn.alpinelinux.org/alpine/v3.7/community add \
    curl \
    php7 \
    php7-json \
    php7-iconv \
    php7-phar \
    php7-mbstring \
    php7-openssl \
    php7-tokenizer \
    php7-simplexml \
    php7-ctype \
    php7-xml \
    && curl -o /tmp/composer-setup.php https://getcomposer.org/installer \
    && curl -o /tmp/composer-setup.sig https://composer.github.io/installer.sig \
    && php -r "if (hash('SHA384', file_get_contents('/tmp/composer-setup.php')) !== trim(file_get_contents('/tmp/composer-setup.sig'))) { echo 'Invalid installer' . PHP_EOL; exit(1); }" \
    && php /tmp/composer-setup.php --no-ansi --install-dir=/usr/local/bin --filename=composer \
    && php -r "unlink('/tmp/composer-setup.php');" \
    && php -r "unlink('/tmp/composer-setup.sig');" \
    && echo "memory_limit=-1" > /etc/php7/conf.d/99_memory-limit.ini \
    && apk del curl \
    && rm -rf /var/cache/apk/* /var/tmp/* /tmp/*

VOLUME ["/app"]
WORKDIR /app

ENTRYPOINT ["phpstan"]
