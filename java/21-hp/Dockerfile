FROM ubuntu:22.04

LABEL author="Adoptium + Pterodactyl Integration"
LABEL org.opencontainers.image.source="https://github.com/Adoptium/containers/"
LABEL org.opencontainers.image.licenses="Apache-2.0"

ENV JAVA_HOME=/opt/java/openjdk
ENV PATH=$JAVA_HOME/bin:$PATH
ENV LANG='en_US.UTF-8' LANGUAGE='en_US:en' LC_ALL='en_US.UTF-8'
ENV TZ=Asia/Taipei

# 安裝必要套件
RUN set -eux; \
    apt-get update; \
    DEBIAN_FRONTEND=noninteractive apt-get install -y --no-install-recommends \
        curl wget gnupg fontconfig \
        ca-certificates p11-kit binutils tzdata \
        locales locales-all \
        lsof openssl git tar sqlite3 iproute2 libstdc++6 \
    && echo "en_US.UTF-8 UTF-8" >> /etc/locale.gen \
    && locale-gen en_US.UTF-8 \
    && update-locale LANG=en_US.UTF-8 \
    && rm -rf /var/lib/apt/lists/*

# 安裝 Temurin JDK 21
ENV JAVA_VERSION=jdk-21.0.8+9
RUN set -eux; \
    ARCH="$(dpkg --print-architecture)"; \
    case "${ARCH}" in \
        amd64) \
            ESUM='f2dc5418092c43003db8f9005c4a286e1c0104fea96ccdd49e8ebd037cac9219'; \
            BINARY_URL='https://github.com/adoptium/temurin21-binaries/releases/download/jdk-21.0.8%2B9/OpenJDK21U-jdk_x64_linux_hotspot_21.0.8_9.tar.gz'; \
            ;; \
        arm64) \
            ESUM='e5c41a1ab0865ea5de9b4529bf8526005f1d4593090845387d14fe450ce39c33'; \
            BINARY_URL='https://github.com/adoptium/temurin21-binaries/releases/download/jdk-21.0.8%2B9/OpenJDK21U-jdk_aarch64_linux_hotspot_21.0.8_9.tar.gz'; \
            ;; \
        *) echo "Unsupported arch: $ARCH"; exit 1 ;; \
    esac; \
    wget -O /tmp/openjdk.tar.gz "$BINARY_URL"; \
    wget -O /tmp/openjdk.tar.gz.sig "$BINARY_URL.sig"; \
    export GNUPGHOME="$(mktemp -d)"; \
    gpg --batch --keyserver keyserver.ubuntu.com --recv-keys 3B04D753C9050D9A5D343F39843C48A565F8F04B; \
    gpg --batch --verify /tmp/openjdk.tar.gz.sig /tmp/openjdk.tar.gz; \
    rm -rf "$GNUPGHOME" /tmp/openjdk.tar.gz.sig; \
    echo "$ESUM  /tmp/openjdk.tar.gz" | sha256sum -c -; \
    mkdir -p "$JAVA_HOME"; \
    tar --extract --file /tmp/openjdk.tar.gz --directory "$JAVA_HOME" --strip-components=1 --no-same-owner; \
    rm /tmp/openjdk.tar.gz "$JAVA_HOME/lib/src.zip"; \
    find "$JAVA_HOME/lib" -name '*.so' -exec dirname '{}' ';' | sort -u > /etc/ld.so.conf.d/docker-openjdk.conf; \
    ldconfig; \
    java -Xshare:dump || true

# 建立容器用戶
RUN useradd -d /home/container -m container

# 複製 entrypoint.sh 並設定權限（此處還是 root）
COPY entrypoint.sh /entrypoint.sh
RUN chmod +x /entrypoint.sh

# 切換到非 root 用戶與目錄
USER container
ENV USER=container HOME=/home/container
WORKDIR /home/container

CMD [ "/bin/bash", "/entrypoint.sh" ]
