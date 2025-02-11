FROM frolvlad/alpine-glibc

ARG REDOT_VERSION
ARG REDOT_TARGET

LABEL org.opencontainers.image.source="https://github.com/Redot-Engine/redocker"
LABEL org.opencontainers.image.description="A CI/CD Image for building Redot $REDOT_VERSION Games for $REDOT_TARGET"

ADD redot /usr/local/bin/redot

RUN mkdir -p /root/.local/share/redot/export_templates/$REDOT_VERSION.stable
ADD templates/version.txt /root/.local/share/redot/export_templates/$REDOT_VERSION.stable/
ADD templates/*$REDOT_TARGET* /root/.local/share/redot/export_templates/$REDOT_VERSION.stable/

RUN case "$REDOT_TARGET" in \
  "android") \
    apk add --no-cache \
      java-jdk \
    ;; \
  esac
