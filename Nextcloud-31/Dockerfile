FROM nextcloud:31.0.2-fpm-alpine

# Update and install additional dependencies
RUN apk update && \
    apk add --no-cache \
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
        rsync \
        bzip2 \
        gnupg \
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
        build-base \
        krb5-dev \
        openssl-dev && \
    rm -rf /var/cache/apk/*

# Build and install libc-client
RUN curl -fsSL https://www.washington.edu/imap/imap-2007f.tar.gz -o imap.tar.gz && \
    tar -xzf imap.tar.gz && \
    cd imap-2007f && \
    make ldb EXTRACFLAGS=-fPIC && \
    mkdir -p /usr/local/lib && \
    cp c-client/*.h /usr/local/include && \
    cp c-client/*.c /usr/local/lib && \
    cp c-client/c-client.a /usr/local/lib/libc-client.a && \
    cd .. && \
    rm -rf imap-2007f imap.tar.gz

# Install PHP extensions
RUN apk add --no-cache --virtual .build-deps \
        $PHPIZE_DEPS \
        imap-dev \
        samba-dev \
        bzip2-dev \
        libpq-dev \
        autoconf \
        freetype-dev \
        gmp-dev \
        icu-dev \
        imagemagick-dev \
        libevent-dev \
        libjpeg-turbo-dev \
        libmcrypt-dev \
        libmemcached-dev \
        libpng-dev \
        libwebp-dev \
        libxml2-dev \
        libzip-dev \
        openldap-dev \
        pcre-dev \
        postgresql-dev \
    ; \
    docker-php-ext-configure imap --with-kerberos --with-imap-ssl; \
    docker-php-ext-configure gd --with-freetype --with-jpeg --with-webp; \
    docker-php-ext-configure ldap; \
    docker-php-ext-install \
        bz2 \
        imap \
        pgsql \
        ftp \
        bcmath \
        exif \
        gd \
        gmp \
        intl \
        ldap \
        opcache \
        pcntl \
        pdo_pgsql \
        sysvsem \
        zip \
    ; \
    pecl install smbclient; \
    docker-php-ext-enable smbclient; \
    apk del .build-deps