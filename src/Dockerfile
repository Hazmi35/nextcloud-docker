# TAGS: latest
# VARIANT:
# PLATFORMS: linux/amd64, linux/arm64
FROM docker.io/library/nextcloud:31.0.0

# Install static build ffmpeg
COPY --from=docker.io/mwader/static-ffmpeg:7.1 /ffmpeg /usr/local/bin/
COPY --from=docker.io/mwader/static-ffmpeg:7.1 /ffprobe /usr/local/bin/

# Install bz2 and smbclient php module
RUN apt-get update -y \
    && apt-get install -y --no-install-recommends smbclient libsmbclient-dev libbz2-dev \
    && pecl install smbclient \
    && docker-php-ext-enable smbclient \
    && docker-php-ext-install bz2 \
    && apt-get purge -y --auto-remove -o APT::AutoRemove::RecommendsImportant=false \
    && apt-get autoremove -y \
    && apt-get autoclean -y \
    && rm -rf /var/lib/apt/lists/*
