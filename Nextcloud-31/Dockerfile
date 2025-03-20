FROM nextcloud:31.0.2-fpm-alpine

RUN apk update && \
      apk add --no-cache \
      procps \
      samba-client \
      samba-client-libs \
      imagemagick \
      imagemagick-libs \
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
      build-base && \
      rm -rf /var/cache/apk/*

RUN apk add --no-cache --virtual .build-deps \
      $PHPIZE_DEPS \
      autoconf \
      freetype-dev \
      gmp-dev \
      icu-dev \
      imagemagick-dev \
      imagemagick-svg \
      imagemagick-heic \
      imagemagick-tiff \
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
      imap-dev \
      krb5-dev \
      openssl-dev \
      samba-dev \
      bzip2-dev \
      libpq-dev && \
      rm -rf /var/cache/apk/* \
    ; \
    docker-php-ext-configure gd --with-freetype --with-jpeg --with-webp; \
    docker-php-ext-configure ftp --with-openssl-dir=/usr; \
    docker-php-ext-configure ldap; \
    docker-php-ext-configure imap --with-kerberos --with-imap-ssl; \
    docker-php-ext-install -j "$(nproc)" \
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
        bz2 \
        imap \
        pgsql \
        ftp \
    ; \
    pecl install smbclient; \
    docker-php-ext-enable smbclient; \
    pecl install inotify; \
    docker-php-ext-enable inotify

RUN apk del .build-deps

# For LibreSign preview image
#RUN sed -i'' 's|.*<policy domain="coder".*"PDF".*|<policy domain="coder" rights="read \| write" pattern="PDF" />|g' /etc/ImageMagick-6/policy.xml