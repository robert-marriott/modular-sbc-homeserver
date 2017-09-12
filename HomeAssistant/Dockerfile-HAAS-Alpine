###############################################################################
#
#      HomeAssistant.io is a home automation program with a nice GUI
#
###############################################################################
FROM hypriot/rpi-alpine-scratch

ENV HOME=/home/homeassistant

EXPOSE 8123

VOLUME /config

RUN \
apk update && \
apk upgrade && \
apk add \
 bash \
 python3 \
 py-pip \
 gcc \
 make \
 musl-dev \
 git \
 openssl-dev \
 libffi-dev && \
 rm -rf /var/cache/apk/*

RUN \
pip install --upgrade pip && \
pip install --upgrade setuptools && \
pip install \
 pathlib \
 pathlib2 \
 # pycrypto \
 # cryptography \
 # packaging \
 # appdirs \
 # six \
 homeassistant

RUN \
mkdir ${HOME} -p && \
adduser -h ${HOME} -s /bin/bash -u 1001 -G root -D default && \
cd ${HOME} && git clone https://github.com/home-assistant/fabric-home-assistant.git && \
cd fabric-home-assistant && fab deploy -H localhost 2>&1 | tee installation_report.txt

CMD haas --open-ui
# CMD [ "python", "-m", "homeassistant", "--config", "/config" ]
