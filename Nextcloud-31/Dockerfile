FROM nextcloud:31.0.3-fpm-alpine

# Update and install additional dependencies
RUN apk add --no-cache \
        procps \
        samba-client \
        samba-client-libs \
        p7zip \
        nano \
        curl \
        ghostscript \
        iputils \
        ffmpeg \
        libheif \
        librsvg \
        util-linux \
        supervisor \
        bash \
        netcat-openbsd \
        openssl \
        git \
        postgresql-client \
        tzdata \
        sudo \
        grep \
        nodejs \
        bind-tools \
        coreutils \
        krb5-dev \
        libc6-compat \
        imap-dev \
    && rm -rf /var/cache/apk/*

# Install additional PHP extensions
RUN apk add --no-cache --virtual .build-deps \
        $PHPIZE_DEPS \
        samba-dev \
        bzip2-dev \
        libpq-dev \
        imap-dev \
    ; \
    docker-php-ext-configure imap --with-kerberos --with-imap-ssl; \
    docker-php-ext-install \
        bz2 \
        imap \
        pgsql \
    ; \
    pecl install smbclient; \
    docker-php-ext-enable smbclient; \
    apk del .build-deps