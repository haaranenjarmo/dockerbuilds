FROM alpine:3.11

ENV PS_VER=7
ENV PS_URL=https://github.com/PowerShell/PowerShell/releases/download/v${PS_VER}.0.0/powershell-${PS_VER}.0.0-linux-alpine-x64.tar.gz
ENV PS_TEMP_FILE=/tmp/powershell.tar.gz
ENV PS_HOME=/opt/microsoft/powershell/${PS_VER}
ENV PS_BIN=${PS_HOME}/pwsh

RUN apk add --no-cache \
    ca-certificates \
    less \
    ncurses-terminfo-base \
    krb5-libs \
    libgcc \
    libintl \
    libssl1.1 \
    libstdc++ \
    tzdata \
    userspace-rcu \
    zlib \
    icu-libs \
    curl

#Add lttng-ust package from alpine/edge repo
RUN apk -X https://dl-cdn.alpinelinux.org/alpine/edge/main add --no-cache lttng-ust

#Install PowerShell
RUN curl -L ${PS_URL} -o ${PS_TEMP_FILE} \
    && mkdir -p ${PS_HOME} \
    && tar zxf ${PS_TEMP_FILE} -C ${PS_HOME} \
    && rm -f ${PS_TEMP_FILE} \
    && chmod +x ${PS_BIN} \
    && ln -s ${PS_BIN} /usr/bin/pwsh

#Set PSGallery as trusted repository and install Azure modules to all users scope
RUN pwsh -NoProfile -ExecutionPolicy ByPass -Command Set-PSRepository -Name PSGallery -InstallationPolicy Trusted \
    && pwsh -NoProfile -ExecutionPolicy ByPass -Command Install-Module -Name Az -Scope AllUsers
