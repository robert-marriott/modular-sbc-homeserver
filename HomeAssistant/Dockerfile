###############################################################################
#
#      HomeAssistant.io is a home automation program with a nice GUI
#
###############################################################################
FROM arm32v7/debian:jessie-slim

ENV HOME=/home/homeassistant

# Expose the port used for the webUI
EXPOSE 8123

# VOLUME /config

# Add basic build dependencies
RUN apt-get update && \
    apt-get upgrade -y && \
    apt-get install -y python3-pip \
      python3-dev \
      python3-yaml \
      libyaml-dev && \
    pip3 install --upgrade \
      pip \
      sqlalchemy \
      aiohttp_cors \
      netdisco \
      xmltodict \
      virtualenv

# Create system user for running haas
RUN adduser --system homeassistant && \
    addgroup homeassistant && \
    mkdir /srv/homeassistant && \
# If you need Zwave support
    usermod -G dialout -a homeassistant

# Create and activate python virtualenv. It is just a folder.
RUN cd /srv/homeassistant && \
    virtualenv -p python3 /srv/homeassistant && \
    /bin/bash -c "source /srv/homeassistant/bin/activate" && \
    pip3 install --upgrade homeassistant && \
    chown -R homeassistant /srv/homeassistant

# Switch to homeassistnat user for virtualenvironment and such
USER homeassistant

CMD hass --open-ui
