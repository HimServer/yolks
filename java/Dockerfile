# 使用 Oracle 官方 GraalVM CE 21 為基礎映像
FROM container-registry.oracle.com/graalvm/jdk:21-ol9

LABEL author="sersoid"
LABEL org.opencontainers.image.source="https://github.com/HimServer/yolks/"
LABEL org.opencontainers.image.licenses=MIT

# 安裝常用工具、字型、locale、台灣時區等
USER root

RUN microdnf install -y \
    tzdata \
    git \
    curl \
    fontconfig \
    freetype \
    lsof \
    ca-certificates \
    iproute \
    sqlite \
    tar \
    gcc \
    make \
    glibc-langpack-en \
    glibc-langpack-zh \
    && ln -sf /usr/share/zoneinfo/Asia/Taipei /etc/localtime \
    && echo "Asia/Taipei" > /etc/timezone \
    && microdnf clean all

ENV LANG en_US.UTF-8
ENV LANGUAGE en_US:en
ENV LC_ALL en_US.UTF-8

# 建立容器使用者
RUN useradd -d /home/container -m container

USER container
ENV USER=container HOME=/home/container
WORKDIR /home/container

COPY ../../entrypoint.sh /entrypoint.sh
CMD [ "/bin/bash", "/entrypoint.sh" ]
