FROM nextcloud:31.0.2-fpm-alpine

RUN apk update && \
      apk add --no-cache \
      procps \
      samba-client \
      samba-client-libs \
      imagemagick \
      imagemagick-libs \
      unrar \
      p7zip \
      p7zip-full \
      nano \
      curl \
      ghostscript \
      openldap-dev \
      iputils \
      ffmpeg \
      libheif \
      librsvg \
      util-linux \
      rsync && \
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