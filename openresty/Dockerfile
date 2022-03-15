FROM alyxbut/openresty:1.19.9.1

LABEL maintainer="Commune WP <docker@commune.host>"

RUN apk add --no-cache --virtual .build-deps \
        git \
        && cd /usr/local/openresty/site/lualib \
        && git clone https://github.com/alyx/simon.git \
        && rm -rf simon/.git \
        && opm get jxskiss/ssl-cert-server \
        && apk del .build-deps

