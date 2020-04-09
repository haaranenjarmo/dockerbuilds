FROM jarmohaaranen/alpine/powershell:latest

LABEL Author="Jarmo Haaranen" \
    Twitter="@HaaranenJarmo" \
    Email="jarmo@haaranen.net"

#Python
ENV PYTHONUNBUFFERED=1

#Install pip3 and it's depencies
##Copied mainly here https://github.com/Docker-Hub-frolvlad/docker-alpine-python3/blob/master/Dockerfile

RUN echo "**** install Python ****" && \
    apk add --no-cache python3 && \
    if [ ! -e /usr/bin/python ]; then ln -sf python3 /usr/bin/python ; fi && \
    \
    echo "**** install pip ****" && \
    python3 -m ensurepip && \
    rm -r /usr/lib/python*/ensurepip && \
    pip3 install --no-cache --upgrade pip setuptools wheel && \
    if [ ! -e /usr/bin/pip ]; then ln -s pip3 /usr/bin/pip ; fi && \
    apk --update add python3-dev libffi-dev openssl-dev build-base

RUN pip3 install --upgrade pip cffi && \
    pip3 install ansible[azure] && \
    pip3 install pywinrm