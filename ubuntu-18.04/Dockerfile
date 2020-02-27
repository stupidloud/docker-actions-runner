FROM ubuntu:latest

RUN groupadd -r runner && useradd -r -g runner runner -m

RUN apt-get update \
    && apt-get install -y --no-install-recommends sudo ca-certificates curl wget repo git jq
RUN apt-get -y install --no-install-recommends bc build-essential asciidoc binutils bzip2 gawk gettext git libncurses5-dev libz-dev patch unzip zlib1g-dev lib32gcc1 libc6-dev-i386 subversion flex uglifyjs git-core gcc-multilib p7zip p7zip-full msmtp libssl-dev texinfo libglib2.0-dev xmlto qemu-utils upx libelf-dev autoconf automake libtool autopoint device-tree-compiler
RUN curl https://raw.githubusercontent.com/friendlyarm/build-env-on-ubuntu-bionic/master/install.sh | bash && rm -rf /var/lib/apt/lists/*

RUN echo 'runner ALL=(ALL) NOPASSWD: ALL' >> /etc/sudoers


WORKDIR /actions-runner

ENV RUNNER_VERSION 2.165.2

RUN curl -L -O https://github.com/actions/runner/releases/download/v${RUNNER_VERSION}/actions-runner-linux-x64-${RUNNER_VERSION}.tar.gz \
    && tar -zxf actions-runner-linux-x64-${RUNNER_VERSION}.tar.gz \
    && rm -f actions-runner-linux-x64-${RUNNER_VERSION}.tar.gz \
    && chown -R runner:runner /actions-runner

COPY ./entrypoint.sh /

ENTRYPOINT ["/entrypoint.sh"]

USER runner
