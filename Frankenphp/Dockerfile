FROM dunglas/frankenphp:1.6.0-builder-alpine AS builder

# Copy xcaddy in the builder image
COPY --from=caddy:builder /usr/bin/xcaddy /usr/bin/xcaddy

# CGO must be enabled to build FrankenPHP
RUN CGO_ENABLED=1 \
    XCADDY_SETCAP=1 \
    XCADDY_GO_BUILD_FLAGS="-ldflags='-w -s' -tags=nobadger,nomysql,nopgx" \
    CGO_CFLAGS=$(php-config --includes) \
    CGO_LDFLAGS="$(php-config --ldflags) $(php-config --libs)" \
    xcaddy build \
        --output /usr/local/bin/frankenphp \
        --with github.com/dunglas/frankenphp=./ \
        --with github.com/dunglas/frankenphp/caddy=./caddy/ \
        --with github.com/dunglas/caddy-cbrotli \
        # Mercure and Vulcain are included in the official build, but feel free to remove them
        --with github.com/dunglas/mercure/caddy \
        --with github.com/dunglas/vulcain/caddy \
        # Add extra Caddy modules here
        --with github.com/caddyserver/nginx-adapter \
        --with github.com/caddy-dns/cloudflare

FROM dunglas/frankenphp:1.6.0-alpine AS runner

# add additional extensions here:
RUN install-php-extensions \
    ctype \
    curl \
    dom \
    fileinfo \
    filter \
    gd \
    hash \
    json \
    libxml \
    mbstring \
    openssl \
    posix \
    session \
    simplexml \
    xmlreader \
    xmlwriter \
    zip \
    zlib \
    pdo_sqlite \
    pdo_mysql \
    pdo_pgsql \
    intl \
    sodium \
    ldap \
    smbclient \
    ftp \
    imap \
    gmp \
    exif \
    apcu \
    memcached \
    redis \
    imagick \
    pcntl \
    phar \
    sysvsem

# Replace the official binary by the one containing your custom modules
COPY --from=builder /usr/local/bin/frankenphp /usr/local/bin/frankenphp