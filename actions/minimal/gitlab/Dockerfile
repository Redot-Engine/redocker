ARG REDOT_VERSION
ARG REDOT_TARGET
FROM ghcr.io/redot-engine/redocker/minimal/${REDOT_TARGET}-${REDOT_VERSION}

LABEL org.opencontainers.image.source="https://github.com/Redot-Engine/redocker"
LABEL org.opencontainers.image.description="A CI/CD Image for building Redot $REDOT_VERSION Games for $REDOT_TARGET in Gitlab CI"

RUN apk add --update --no-cache \
  ca-certificates \
  openssl \
  openssh-client \
  git \
  git-lfs \
  wget \
  curl \
  tar \
  zip \
  unzip \
  xz \
  zstd \
  parallel

CMD ["/bin/sh"]
