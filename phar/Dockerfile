FROM alpine:3.7

ENV PHPSTAN_VERSION 0.9

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
    php7-zlib \
    && curl -LOs https://github.com/phpstan/phpstan/releases/download/$PHPSTAN_VERSION/phpstan.phar \
    && chmod +x phpstan.phar \
    && mv phpstan.phar /usr/local/bin/phpstan \
    && apk del curl \
    && rm -rf /var/cache/apk/* /var/tmp/* /tmp/*

VOLUME ["/app"]
WORKDIR /app

ENTRYPOINT ["php", "-d", "memory_limit=-1", "/usr/local/bin/phpstan"]
