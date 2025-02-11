ARG REDOT_VERSION
ARG REDOT_TARGET
FROM ghcr.io/redot-engine/redocker/minimal/${REDOT_TARGET}-${REDOT_VERSION}

LABEL org.opencontainers.image.source="https://github.com/Redot-Engine/redocker"
LABEL org.opencontainers.image.description="A CI/CD Image for building Redot $REDOT_VERSION Games for $REDOT_TARGET in Github Actions"

RUN apk add --update --no-cache \
  sudo \
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
  jq \
  parallel \
  bash \
  nodejs \
  npm \
  github-cli

RUN adduser -D runner \
   && echo "runner ALL=(ALL) NOPASSWD: ALL" > /etc/sudoers.d/runner \
   && chmod 0440 /etc/sudoers.d/runner
RUN chmod -R 777 /opt
WORKDIR /github/workspace

CMD ["/bin/bash"]
USER runner
