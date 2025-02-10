###########################
##      Build Stage      ##
###########################
FROM alpine:latest AS build-stage

ARG REDOT_VERSION

RUN apk add --no-cache curl

RUN wget $( \
        curl -s https://api.github.com/repos/Redot-Engine/redot-engine/releases/tags/redot-$REDOT_VERSION-stable \
        | grep "browser_download_url.*Redot_v.*-stable_export_templates\.tpz" \
        | cut -d '"' -f 4 - \
        | head -n 1 \
    ) -O Redot_Export_Templates.tbz

RUN unzip Redot_Export_Templates.tbz

# Delete Debug Export Templates
RUN rm -f templates/*debug*

RUN rm Redot_Export_Templates.tbz

###########################
##      Final Stage      ##
###########################
FROM frolvlad/alpine-glibc AS final-stage

ARG REDOT_VERSION
ARG REDOT_TARGET

LABEL org.opencontainers.image.source="https://github.com/Redot-Engine/redocker"
LABEL org.opencontainers.image.description="A CI/CD Image for building Redot $REDOT_VERSION Games for $REDOT_TARGET"

# Docker deps
RUN apk add --update --no-cache \
  wget \
  curl \
  unzip

ENV PATH="$PATH:/root/.local/bin"

RUN wget $( \
        curl -s https://api.github.com/repos/Redot-Engine/redot-engine/releases/tags/redot-$REDOT_VERSION-stable \
        | grep "browser_download_url.*Redot_v.*-stable_linux\.x86_64\.zip" \
        | cut -d '"' -f 4 - \
        | head -n 1 \
    ) -O Redot.zip \
    && unzip Redot.zip \
    && mv ./Redot_v*-stable_linux.x86_64 /usr/local/bin/redot \
    && rm Redot.zip

RUN mkdir -p /root/.local/share/redot/export_templates/$REDOT_VERSION.stable
COPY --from=build-stage /templates/version.txt /root/.local/share/redot/export_templates/$REDOT_VERSION.stable/
COPY --from=build-stage /templates/*$REDOT_TARGET* /root/.local/share/redot/export_templates/$REDOT_VERSION.stable/
