FROM caddy:2.9.1-builder AS builder

RUN xcaddy build \
    --with github.com/caddyserver/nginx-adapter \
    --with github.com/caddy-dns/cloudflare

RUN apk add --no-cache \
    tzdata \
    ca-certificates \
    libcap \
    mailcap

FROM caddy:2.9.1

COPY --from=builder /usr/bin/caddy /usr/bin/caddy 
