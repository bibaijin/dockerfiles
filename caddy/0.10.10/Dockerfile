FROM bibaijin/debian:stretch

ENV CADDY_VERSION=0.10.10

WORKDIR /app

RUN mkdir -p /tmp \
    && cd /tmp \
    && curl -sSL https://github.com/mholt/caddy/releases/download/v${CADDY_VERSION}/caddy_v${CADDY_VERSION}_linux_amd64.tar.gz -o caddy.tar.gz \
    && tar xzf caddy.tar.gz \
    && mv caddy /app \
    && rm -rf /tmp/*

EXPOSE 80 443 2015
CMD ["/app/caddy"]