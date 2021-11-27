FROM alpine:3.14

ENV JAVA_VERSION 8

ENV LANG en_US.UTF-8
ENV LANGUAGE en_US:en
ENV LC_ALL en_US.UTF-8

RUN apk add --no-cache --update curl ca-certificates openssl git tar fontconfig tzdata sqlite iproute2 bash \
    && adduser --disabled-password --home /home/container container

RUN wget -P /etc/apk/keys/ \
    https://cdn.azul.com/public_keys/alpine-signing@azul.com-5d5dc44c.rsa.pub && \
    echo "https://repos.azul.com/zulu/alpine" >> /etc/apk/repositories && \
    apk --no-cache add zulu$JAVA_VERSION-ca-jre-headless

ENV JAVA_HOME=/usr/lib/jvm/zulu$JAVA_VERSION-ca

USER container
ENV  USER=container HOME=/home/container

WORKDIR /home/container

COPY ./entrypoint.sh /entrypoint.sh

CMD ["/bin/bash", "/entrypoint.sh"]