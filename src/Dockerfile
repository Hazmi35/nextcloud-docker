# TAGS: latest
# PLATFORMS: linux/amd64, linux/arm64
FROM docker.io/library/nextcloud:35.0.3@sha256:f44180601f18e7664557232b4c5edb0eb4a82d649c05b93313f4e15909553d42 AS base

FROM base AS builder

# Install build dependencies and compile PHP extensions
RUN apt-get update && apt-get install -y --no-install-recommends \
        libsmbclient-dev \
    && pecl install smbclient \
    && docker-php-ext-enable smbclient \
    && rm -rf /var/lib/apt/lists/*

FROM base AS final

# Copy static ffmpeg binaries from a specific, verified source.
COPY --from=docker.io/mwader/static-ffmpeg:7.1@sha256:a8090df5f5608daef387e1b2e93b98aaacb4d92153ad904e7d715c725724fca4 /ffmpeg /usr/local/bin/
COPY --from=docker.io/mwader/static-ffmpeg:7.1@sha256:a8090df5f5608daef387e1b2e93b98aaacb4d92153ad904e7d715c725724fca4 /ffprobe /usr/local/bin/

# Copy compiled extensions from builder stage
COPY --from=builder /usr/local/etc/php/conf.d/ /usr/local/etc/php/conf.d/
COPY --from=builder /usr/local/lib/php/extensions/ /usr/local/lib/php/extensions/

# Install runtime dependencies and verify extensions
RUN apt-get update && apt-get install -y --no-install-recommends \
        smbclient \
        curl \
    && rm -rf /var/lib/apt/lists/* \
    && php -m | grep -i smbclient
