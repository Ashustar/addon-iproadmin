ARG BUILD_FROM=hassioaddons/base:8.0.5
# hadolint ignore=DL3006
FROM ${BUILD_FROM}

# Set shell
SHELL ["/bin/bash", "-o", "pipefail", "-c"]

# Setup base
RUN \
    apk add --no-cache \
        nginx=1.18.0-r1 \
        php7-curl=7.3.23-r0 \
        php7-fpm=7.3.23-r0 \
        php7-json=7.3.23-r0 \
        php7-opcache=7.3.23-r00 \
        php7-session=7.3.23-r0 \
        php7-zip=7.3.23-r0 \
        php7=7.3.23-r0 \
    \
    && apk add --no-cache --virtual .build-dependencies \
        git=2.26.2-r0 \
    \
    && git clone --branch v1.1.1 --depth=1 \
        https://github.com/Ashustar/iproAdmin.git /var/www/tasmoadmin \
    \
    && apk del --no-cache --purge .build-dependencies \
    \
    && rm -f -r /var/www/tasmoadmin/.git \
    && rm -f -r /var/www/tasmoadmin/portable \
    && find /var/www/tasmoadmin -type f -name ".htaccess" -depth -exec rm -f {} \; \
    && find /var/www/tasmoadmin -type f -name "*.md" -depth -exec rm -f {} \; \
    && find /var/www/tasmoadmin -type f -name ".gitignore" -depth -exec rm -f {} \; \
    && find /var/www/tasmoadmin -type f -name ".empty" -depth -exec rm -f {} \;

# Copy root filesystem
COPY rootfs /

# Build arguments
ARG BUILD_ARCH
ARG BUILD_DATE
ARG BUILD_REF
ARG BUILD_VERSION

# Labels
LABEL \
    io.hass.name="IPro Admin" \
    io.hass.description="Centrally manage all your IPro Smart Devices" \
    io.hass.arch="${BUILD_ARCH}" \
    io.hass.type="addon" \
    io.hass.version=${BUILD_VERSION} \
    maintainer="SPELEC" \
    org.opencontainers.image.title="IPRO Admin" \
    org.opencontainers.image.description="Centrally manage all your IPRO devices" \
    org.opencontainers.image.vendor="Home Assistant Community Add-ons" \
    org.opencontainers.image.authors="SPELEC" \
    org.opencontainers.image.licenses="MIT" \
    org.opencontainers.image.url="https://spelec.in" \
    org.opencontainers.image.source="https://github.com/Ashustar/addon-iproadmin" \
    org.opencontainers.image.documentation="https://github.com/Ashustar/addon-iproadmin/blob/master/README.md" \
    org.opencontainers.image.created=${BUILD_DATE} \
    org.opencontainers.image.revision=${BUILD_REF} \
    org.opencontainers.image.version=${BUILD_VERSION}
