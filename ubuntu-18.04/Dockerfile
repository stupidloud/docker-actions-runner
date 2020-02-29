FROM ubuntu:18.04

RUN groupadd -r runner && useradd -r -g runner runner -m

RUN apt-get update \
    && apt-get install -y --no-install-recommends sudo parted dosfstools rsync wget ca-certificates curl git jq bc build-essential asciidoc binutils bzip2 gawk gettext git libncurses5-dev libz-dev patch unzip zlib1g-dev lib32gcc1 libc6-dev-i386 subversion flex uglifyjs git-core gcc-multilib p7zip p7zip-full msmtp libssl-dev texinfo libglib2.0-dev xmlto qemu-utils upx libelf-dev autoconf automake libtool autopoint device-tree-compiler bison g++-multilib git gperf libxml2-utils make python-networkx zip flex curl libncurses5-dev libssl-dev zlib1g-dev gawk minicom openjdk-8-jdk device-tree-compiler liblz4-tool bison openssh-server vim qemu-user-static exfat-fuse exfat-utils p7zip-full tree autoconf libcurl4-openssl-dev libssh-dev pkg-config libelf-dev libtool libqt5core5a libqt5gui5 libqt5opengl5 libqt5printsupport5 libqt5widgets5 libqt5x11extras5 libsdl1.2debian texinfo genext2fs lzip help2man libtool libtool-bin debootstrap u-boot-tools swig python-dev python3-dev ack-grep repo time gettext java-propose-classpath android-tools-fsutils bc lzop xfonts-utils xfonts-utils xfonts-utils xsltproc libjson-perl \
    && rm -rf /var/lib/apt/lists/*

RUN echo 'runner ALL=(ALL) NOPASSWD: ALL' >> /etc/sudoers

WORKDIR /actions-runner

ENV RUNNER_VERSION 2.165.2

RUN curl -L https://github.com/actions/runner/releases/download/v${RUNNER_VERSION}/actions-runner-linux-x64-${RUNNER_VERSION}.tar.gz | tar xz \
    && chown -R runner:runner /actions-runner

COPY ./entrypoint.sh /

ENTRYPOINT ["/entrypoint.sh"]

USER runner
