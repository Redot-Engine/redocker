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

LABEL org.opencontainers.image.source=https://github.com/Redot-Engine/redocker


RUN apk add --update --no-cache \
bash sudo ca-certificates openssl openssh-client \
git git-lfs wget curl \
tar zip unzip xz zstd jq \
nodejs npm python3 py3-pip parallel

RUN adduser -D runner \
   && echo "runner ALL=(ALL) NOPASSWD: ALL" > /etc/sudoers.d/runner \
   && chmod 0440 /etc/sudoers.d/runner
RUN chmod -R 777 /opt
WORKDIR /home/runner

CMD ["/bin/bash"]
USER runner

ARG REDOT_VERSION
ARG REDOT_TARGET

# fontconfig and eudev-dev are not needed in ci, and will segfault
RUN sudo apk add --no-cache \
  scons \
  pkgconf \
  gcc \
  g++ \
  libx11-dev \
  libxcursor-dev \
  libxinerama-dev \
  libxi-dev \
  libxrandr-dev \
  mesa-dev \
  alsa-lib-dev \
  pulseaudio-dev \
  pipx

RUN pipx install "gdtoolkit==$REDOT_VERSION.*"

ENV PATH="$PATH:/home/runner/.local/bin"

RUN wget $( \
        curl -s https://api.github.com/repos/Redot-Engine/redot-engine/releases/tags/redot-$REDOT_VERSION-stable \
        | grep "browser_download_url.*Redot_v.*-stable_linux\.x86_64\.zip" \
        | cut -d '"' -f 4 - \
        | head -n 1 \
    ) -O Redot.zip \
    && sudo unzip Redot.zip \
    && sudo mv ./Redot_v*-stable_linux.x86_64 /usr/local/bin/redot \
    && rm Redot.zip

RUN mkdir -p /home/runner/.local/share/redot/export_templates/$REDOT_VERSION.stable
COPY --from=build-stage /templates/version.txt /home/runner/.local/share/redot/export_templates/$REDOT_VERSION.stable/
COPY --from=build-stage /templates/*$REDOT_TARGET* /home/runner/.local/share/redot/export_templates/$REDOT_VERSION.stable/