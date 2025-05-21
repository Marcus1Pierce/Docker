FROM dunglas/frankenphp:1.6.0-builder-alpine AS builder

# Install PHP development tools for `php-config`
RUN apk add --no-cache php-dev php-config build-base

# Copy xcaddy in the builder image
COPY --from=caddy:builder /usr/bin/xcaddy /usr/bin/xcaddy

# CGO must be enabled to build FrankenPHP
RUN CGO_ENABLED=1 \
    XCADDY_SETCAP=1 \
    XCADDY_GO_BUILD_FLAGS="-ldflags='-w -s' -tags=nobadger,nomysql,nopgx" \
    CGO_CFLAGS=$(php-config --includes) \
    CGO_LDFLAGS="$(php-config --ldflags) $(php-config --libs)" \
    echo "CGO_CFLAGS: $CGO_CFLAGS" && \
    echo "CGO_LDFLAGS: $CGO_LDFLAGS" && \
    xcaddy build \
        --output /usr/local/bin/frankenphp \
        --with github.com/caddyserver/nginx-adapter \
        --with github.com/caddy-dns/cloudflare

FROM dunglas/frankenphp:1.6.0-alpine AS runner

# Replace the official binary by the one containing your custom modules
COPY --from=builder /usr/local/bin/frankenphp /usr/local/bin/frankenphp