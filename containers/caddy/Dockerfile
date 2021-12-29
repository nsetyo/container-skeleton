ARG CADDY_VERSION=2

FROM caddy:${CADDY_VERSION}-builder-alpine AS caddy-builder

RUN xcaddy build

FROM caddy:${CADDY_VERSION} AS caddy

WORKDIR /var/www

COPY --from=caddy-builder /usr/bin/caddy /usr/bin/caddy