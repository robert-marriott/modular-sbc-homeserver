###############################################################################
#
#      HomeAssistant.io is a home automation program with a nice GUI
#
###############################################################################
# FROM hypriot/rpi-alpine-scratch
FROM arm32v7/debian:jessie-slim

ENV HOME=/home/homeassistant
EXPOSE 8123

# VOLUME /config

# Add basic build dependencies
RUN apt-get update && \
    apt-get upgrade -y && \
    apt-get install -y apt-utils python3-pip python3-dev && \
    pip3 install --upgrade virtualenv

# Create system user for running haas
RUN adduser --system homeassistant && \
    addgroup homeassistant && \
    mkdir /srv/homeassistant && \
    chown -R homeassistant /srv/homeassistant && \
# If you need Zwave support
    usermod -G dialout -a homeassistant

# Switch to homeassistnat user for virtualenvironment and such
USER homeassistant

# Create and activate python virtualenv. It is just a folder.
RUN cd /srv/homeassistant && \
    virtualenv -p python3 /srv/homeassistant && \
    source /srv/homeassistant/bin/activate && \
    pip3 install --upgrade homeassistant

CMD /srv/homeassistant/bin/hass --open-ui

# RUN \
# apk update && \
# apk upgrade && \
# apk add \
#  bash \
#  python3 \
#  py-pip \
#  gcc \
#  make \
#  musl-dev \
#  git \
#  openssl-dev \
#  libffi-dev && \
#  rm -rf /var/cache/apk/*
#
# RUN \
# pip install --upgrade pip && \
# pip install --upgrade setuptools && \
# pip install \
#  pathlib \
#  pathlib2 \
#  # pycrypto \
#  # cryptography \
#  # packaging \
#  # appdirs \
#  # six \
#  homeassistant
#
# RUN \
# mkdir ${HOME} -p && \
# adduser -h ${HOME} -s /bin/bash -u 1001 -G root -D default && \
# cd ${HOME} && git clone https://github.com/home-assistant/fabric-home-assistant.git && \
# cd fabric-home-assistant && fab deploy -H localhost 2>&1 | tee installation_report.txt

# CMD haas --open-ui
# CMD [ "python", "-m", "homeassistant", "--config", "/config" ]
