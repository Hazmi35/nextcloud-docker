
# TAGS: latest
# VARIANT:
# PLATFORMS: linux/amd64, linux/arm64
FROM docker.io/library/nextcloud:26.0.1

# Install ffmpeg
COPY --from=docker.io/mwader/static-ffmpeg:6.0 /ffmpeg /usr/local/bin/
COPY --from=docker.io/mwader/static-ffmpeg:6.0 /ffprobe /usr/local/bin/

# Install bz2 and smbclient module
RUN apt-get update -y \
    && apt-get install -y --no-install-recommends smbclient libsmbclient-dev libbz2-dev \
    && pecl install smbclient \
    && docker-php-ext-enable smbclient \
    && docker-php-ext-install bz2 \
    && apt-get purge -y --auto-remove -o APT::AutoRemove::RecommendsImportant=false \
    && apt-get autoremove -y \
    && apt-get autoclean -y \
    && rm -rf /var/lib/apt/lists/*
