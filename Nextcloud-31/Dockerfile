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
        openssl-dev \
        libc-client-devel && \
    rm -rf /var/cache/apk/*

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