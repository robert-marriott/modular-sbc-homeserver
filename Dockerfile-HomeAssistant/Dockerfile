###############################################################################
#
#      HomeAssistant.io is a home automation program with a nice GUI
#
###############################################################################
FROM arm32v7/debian:jessie-slim

EXPOSE 8123

RUN \
apt-get update && \
apt-get install -y python3 python3-pip && \
rm -rf /var/lib/apt/lists/*

# useradd -rm homeassistant
# mkdir homeassistant
# chown homeassistant:homeassistant homeassistant

RUN pip3 install homeassistant

CMD hass
