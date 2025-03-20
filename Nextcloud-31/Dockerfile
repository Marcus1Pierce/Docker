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
      openldap-dev \
      iputils \
      ffmpeg \
      libheif \
      librsvg \
      util-linux \
      rsync \
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
      pcre-dev \
      postgresql-dev \
      bzip2 \
      gnupg \
      supervisor \
      imap-dev \
      krb5-dev \
      openssl-dev \
      samba-dev \
      bzip2-dev \
      libpq-dev \
      bash \
      netcat-openbsd \
      openssl \
      git \
      postgresql-client \
      tzdata \
      sudo \
      grep \
      nodejs \
      libreoffice \
      bind-tools \
      coreutils && \
      # Not supported yet python3-pip
      rm -rf /var/cache/apk/*

# Samba client php extension
RUN pecl install smbclient
RUN docker-php-ext-enable smbclient

# Install php-ldap Extension
RUN docker-php-ext-install ldap

# inotify extension
RUN pecl install inotify

# For LibreSign preview image
RUN sed -i'' 's|.*<policy domain="coder".*"PDF".*|<policy domain="coder" rights="read \| write" pattern="PDF" />|g' /etc/ImageMagick-6/policy.xml