FROM --platform=$TARGETOS/$TARGETARCH debian:bullseye

LABEL author="Michael Parker" maintainer="parker@pterodactyl.io"

ENV         DEBIAN_FRONTEND noninteractive

RUN         apt update -y \
         && apt install -y libtesseract-dev iproute2 \
         && useradd -m -d /home/container container

USER        container
ENV         USER=container HOME=/home/container
WORKDIR     /home/container

COPY ./entrypoint.sh /entrypoint.sh
CMD ["/bin/bash", "/entrypoint.sh"]
