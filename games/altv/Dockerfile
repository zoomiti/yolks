# ----------------------------------
# Environment: debian
# ----------------------------------
FROM    --platform=$TARGETOS/$TARGETARCH node:16-bookworm

LABEL   author="goover" maintainer="info@goover.de"

ENV     DEBIAN_FRONTEND noninteractive

RUN     useradd -m -d /home/container -s /bin/bash container

RUN     apt update -y \
        && apt upgrade -y \
        && apt install -y g++ gcc libgcc-s1 lib32gcc-s1 gdb libstdc++6 libc6 git wget curl tar zip unzip binutils xz-utils liblzo2-2 cabextract iproute2 net-tools netcat-traditional telnet libatomic1 libsdl1.2debian libsdl2-2.0-0 \
        libfontconfig1 libicu72 icu-devtools libunwind8 libssl-dev sqlite3 libsqlite3-dev libmariadb-dev libduktape207 locales ffmpeg gnupg2 apt-transport-https software-properties-common ca-certificates tzdata libgdiplus\ 
		python3 dnsutils build-essential coreutils jq pcregrep tini

RUN     wget https://dot.net/v1/dotnet-install.sh \
        && D_V_5="$(curl -sSL https://dotnet.microsoft.com/en-us/download/dotnet/5.0 | grep -i  '<h3 id="sdk-5.*">SDK 5.*.*</h3>'  | head -1 | awk -F\" '{print $3}' | awk '{print $2;}' | sed 's/<\/h3>//g')" \
        && D_V_6="$(curl -sSL https://dotnet.microsoft.com/en-us/download/dotnet/6.0 | grep -i  '<h3 id="sdk-5.*">SDK 6.*.*</h3>'  | head -1 | awk -F\" '{print $3}' | awk '{print $2;}' | sed 's/<\/h3>//g')" \
        && D_V_7="$(curl -sSL https://dotnet.microsoft.com/en-us/download/dotnet/7.0 | grep -i  '<h3 id="sdk-5.*">SDK 7.*.*</h3>'  | head -1 | awk -F\" '{print $3}' | awk '{print $2;}' | sed 's/<\/h3>//g')" \
        && chmod +x dotnet-install.sh \
	&& ./dotnet-install.sh -i /usr/share -v $D_V_5 \
        && ./dotnet-install.sh -i /usr/share -v $D_V_6 \
        && ./dotnet-install.sh -i /usr/share -v $D_V_7 \
        && ln -s /usr/share/dotnet /usr/bin/dotnet

RUN     update-locale lang=en_US.UTF-8 \
        && dpkg-reconfigure --frontend noninteractive locales

USER    container
ENV     USER=container HOME=/home/container
WORKDIR /home/container

STOPSIGNAL SIGINT

COPY        --chown=container:container ./entrypoint.sh /entrypoint.sh
RUN         chmod +x /entrypoint.sh
ENTRYPOINT    ["/usr/bin/tini", "-g", "--"]
CMD         ["/entrypoint.sh"]