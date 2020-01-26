FROM alpine:3.10

LABEL author="Rye Miller" \
      vendor="Darkstar" \
      version="0.1"

ENV PORT /tmp/.newrelic.sock

ARG VERSION=9.4.1.250

ENV AGENT newrelic-php5-${VERSION}-linux-musl
ENV URL https://download.newrelic.com/php_agent/archive/${VERSION}/${AGENT}.tar.gz

RUN \
    set -ex; \
    apk --no-cache add curl; \
    curl --connect-timeout 10 -o nr.tar.gz -fSL ${URL}; \
    tar -xf nr.tar.gz; \
    cp ${AGENT}/daemon/newrelic-daemon.x64 /usr/local/bin/newrelic-daemon; \
    mkdir -p /var/log/newrelic; \
    rm -rf newrelic-php5* nr.tar.gz;

CMD ["sh", "-c", "/usr/local/bin/newrelic-daemon -f --port ${PORT}"]