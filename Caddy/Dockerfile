FROM caddy:2.10.0-builder AS builder

RUN xcaddy build \
    --with github.com/caddyserver/nginx-adapter \
    --with github.com/caddy-dns/cloudflare

FROM caddy:2.10.0

COPY --from=builder /usr/bin/caddy /usr/bin/caddy 
