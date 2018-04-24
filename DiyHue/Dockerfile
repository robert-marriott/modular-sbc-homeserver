###############################################################################
# DiyHue is a Philips Hue bridge emulator by mariusmotea. It has a large
# feature set, and is being dockerized here for use on an arm device.
###############################################################################
FROM armhf/alpine:edge

ENV GPG_KEY=C01E1CAD5EA2C4F0B8E3571504C367C218ADD4FF

# Add dependencies for Linux-Dash to work
RUN  apk update && apk upgrade && \
     apk add  bash \
              nmap \
              python3 \
              git && \
    # clone git repo onto filesystem
    mkdir -p /opt/hue-emulator && \
    git clone https://github.com/mariusmotea/diyHue.git /opt/hue-emulator && \
    cp -R /opt/hue-emulator/BridgeEmulator/* /opt/hue-emulator/ && \
    # Install python modules needed to run scripts
    pip3 install requests ws4py && \
    # Clean up alpine image
    apk del git curl && \
    rm -rf /var/cache/apk/* && \
# Create container unpriveleged base user and diretory structure
    adduser -s /bin/bash -u 1001 -G root -D default && \
    chown -R 1001:0 /opt/hue-emulator && \
    chmod -R 777 /opt/hue-emulator

EXPOSE 80

USER 1001

CMD python3 /opt/hue-emulator/HueEmulator3.py
