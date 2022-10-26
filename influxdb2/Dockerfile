ARG BUILD_FROM=ghcr.io/hassio-addons/debian-base/amd64:6.1.2
# hadolint ignore=DL3006
FROM ${BUILD_FROM}

# Set shell
SHELL ["/bin/bash", "-o", "pipefail", "-c"]

# Setup base system
ARG BUILD_ARCH=amd64

RUN \
    apt-get update \
    && ARCH="${BUILD_ARCH}" \
    && if [ "${BUILD_ARCH}" = "aarch64" ]; then ARCH="arm64"; fi \
    \
    && INFLUXDB="2.4.0" \
    && curl -J -L -o /tmp/influxdb2.deb \
        "https://dl.influxdata.com/influxdb/releases/influxdb2-${INFLUXDB}-${ARCH}.deb" \
    \
    && curl -J -L -o /tmp/influxdb-cli.deb \
        "https://dl.influxdata.com/influxdb/releases/influxdb2-client-${INFLUXDB}-${ARCH}.deb" \
    && dpkg --install /tmp/influxdb2.deb \
    && dpkg --install /tmp/influxdb-cli.deb \
    \
    && rm -fr \
        /tmp/* \
        /var/{cache,log}/* \
        /var/lib/apt/lists/* \
    \
    && mkdir -p /data/influxdb2/engine


# Copy root filesystem
COPY rootfs /

# Build arguments
ARG BUILD_ARCH
ARG BUILD_DATE
ARG BUILD_DESCRIPTION
ARG BUILD_NAME
ARG BUILD_REF
ARG BUILD_REPOSITORY
ARG BUILD_VERSION

# Labels
LABEL \
    io.hass.name="${BUILD_NAME}" \
    io.hass.description="${BUILD_DESCRIPTION}" \
    io.hass.arch="${BUILD_ARCH}" \
    io.hass.type="addon" \
    io.hass.version=${BUILD_VERSION} \
    maintainer="Jay Antoney <jayantoney@gmail.com>" \
    org.opencontainers.image.title="${BUILD_NAME}" \
    org.opencontainers.image.description="${BUILD_DESCRIPTION}" \
    org.opencontainers.image.vendor="Jays Home Assistant Add-ons" \
    org.opencontainers.image.authors="Jay Antoney <jayantoney@gmail.com>" \
    org.opencontainers.image.licenses="MIT" \
    org.opencontainers.image.url="https://github.com/Jays-Home-Assistant-Add-ons" \
    org.opencontainers.image.source="https://github.com/${BUILD_REPOSITORY}" \
    org.opencontainers.image.documentation="https://github.com/${BUILD_REPOSITORY}/blob/main/README.md" \
    org.opencontainers.image.created=${BUILD_DATE} \
    org.opencontainers.image.revision=${BUILD_REF} \
    org.opencontainers.image.version=${BUILD_VERSION}
