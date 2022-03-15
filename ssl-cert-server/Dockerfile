FROM alpine:3.15.0 AS build
LABEL maintainer="Commune WP <docker@commune.host>"
ARG SSLCERTSERVER_VERSION=v0.4.2

RUN apk add --no-cache --virtual .build-deps \
    git \
    go \
    && mkdir /data \
    && cd /tmp \
    && git clone -b ${SSLCERTSERVER_VERSION} https://github.com/jxskiss/ssl-cert-server.git \
    && git clone https://github.com/communewp/ssl-cert-server-env2json.git 

RUN cd /tmp/ssl-cert-server \
    && go build -ldflags "-linkmode external -extldflags -static" -o /ssl-cert-server

RUN cd /tmp/ssl-cert-server-env2json \
    && go build -ldflags "-linkmode external -extldflags -static" -o /env2json 

FROM scratch
LABEL maintainer="Commune WP <docker@commune.host>"
COPY --from=build /ssl-cert-server /
COPY --from=build /env2json /
VOLUME /data
EXPOSE 8999
CMD ["/env2json", "-o", "/config.yml", "-e", "/ssl-cert-server -config=/config.yml"]

