FROM        --platform=$TARGETOS/$TARGETARCH debian:bullseye-slim

LABEL       author="Manuel Dielacher" maintainer="th3dilli@gmx.at"

LABEL       org.opencontainers.image.source="https://github.com/pterodactyl/yolks"
LABEL       org.opencontainers.image.licenses=MIT

RUN			dpkg --add-architecture i386 \
			&& apt update && apt upgrade -y \
			&& apt install -y iproute2 locales lib32gcc-s1 lib32stdc++6 libstdc++5:i386 \
			&& update-locale lang=en_US.UTF-8 \
			&& dpkg-reconfigure --frontend noninteractive locales \
			&& useradd -m -d /home/container -s /bin/bash container

USER        container
ENV         USER=container HOME=/home/container
ENV         DEBIAN_FRONTEND noninteractive

WORKDIR     /home/container

COPY        ./entrypoint.sh /entrypoint.sh
CMD         [ "/bin/bash", "/entrypoint.sh" ]
