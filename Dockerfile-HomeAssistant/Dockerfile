###############################################################################
#
#      HomeAssistant.io is a home automation program with a nice GUI
#
###############################################################################
# FROM arm32v7/debian:jessie-slim
FROM hypriot/rpi-alpine-scratch

ENV HOME=/home/homeassistant

EXPOSE 8123

VOLUME /config

RUN \
apk update && \
apk upgrade && \
apk add \
 bash \
 python-dev \
 python-pip \
 git \
 openssl-dev \
 libffi-dev && \
 rm -rf /var/cache/apk/*

RUN \
pip install --upgrade pip && \
pip install --upgrade setuptools && \
pip install \
 pycrypto \
 cryptography \
 packaging \
 appdirs \
 six \
 fabric

RUN \
mkdir ${HOME} -p && \
adduser -h ${HOME} -s /bin/bash -u 1001 -G root -D default && \
cd ${HOME} && git clone https://github.com/home-assistant/fabric-home-assistant.git && \
cd fabric-home-assistant && fab deploy -H localhost 2>&1 | tee installation_report.txt

CMD haas --open-ui

# # Install hass component dependencies
# COPY requirements_all.txt requirements_all.txt
#
# RUN \
# apt-get install -y curl && \
# curl -O https://raw.githubusercontent.com/home-assistant/fabric-home-assistant/master/hass_rpi_installer.sh && \
# bash hass_rpi_installer.sh
# RUN \
# apt-get update && \
# apt-get install -y python3 python3-pip && \
# rm -rf /var/lib/apt/lists/*

# useradd -rm homeassistant
# mkdir homeassistant
# chown homeassistant:homeassistant homeassistant

# RUN pip3 install Flask-SQLAlchemy homeassistant && \
#     pip3 install --no-cache-dir -r requirements_all.txt && \
#     pip3 install --no-cache-dir mysqlclient psycopg2 uvloop cchardet



# CMD haas --open-ui
# CMD [ "python", "-m", "homeassistant", "--config", "/config" ]
