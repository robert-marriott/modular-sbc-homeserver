###############################################################################
#
#      HomeAssistant.io is a home automation program with a nice GUI
#
###############################################################################
FROM arm32v7/debian:jessie-slim

EXPOSE 8123
VOLUME /config

# Install hass component dependencies
COPY requirements_all.txt requirements_all.txt

RUN \
apt-get update && \
apt-get install -y python3 python3-pip && \
rm -rf /var/lib/apt/lists/*

# useradd -rm homeassistant
# mkdir homeassistant
# chown homeassistant:homeassistant homeassistant

RUN pip3 install Flask-SQLAlchemy homeassistant &&
    pip3 install --no-cache-dir -r requirements_all.txt && \
    pip3 install --no-cache-dir mysqlclient psycopg2 uvloop cchardet

CMD hass --open-ui
# CMD [ "python", "-m", "homeassistant", "--config", "/config" ]
