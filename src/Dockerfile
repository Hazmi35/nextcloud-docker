# TAGS: latest
# VARIANT:
# PLATFORMS: linux/amd64, linux/arm64
FROM docker.io/library/nextcloud:32.0.5@sha256:11a3a4f63bad8813c7455b4a3c473ccd1c41e2c48f55decb51718f15691e7568

# Install static build ffmpeg
COPY --from=docker.io/mwader/static-ffmpeg:7.1@sha256:a8090df5f5608daef387e1b2e93b98aaacb4d92153ad904e7d715c725724fca4 /ffmpeg /usr/local/bin/
COPY --from=docker.io/mwader/static-ffmpeg:7.1@sha256:a8090df5f5608daef387e1b2e93b98aaacb4d92153ad904e7d715c725724fca4 /ffprobe /usr/local/bin/

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
