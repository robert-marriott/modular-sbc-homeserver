###############################################################################
# Pi Hole is a DNS level ad blocker for a network. It forces ad requests
# to resolve to nowhere when they are asked for, without a client side app.
###############################################################################
FROM hypriot/rpi-alpine-scratch

#53 is the DNS server, 80 the web frontend, and 4711 pinhole-FTL
EXPOSE 53 80 4711

# Update package repositories, install, and remove cache.
RUN apk update && \
apk upgrade && \
apk add \
 bash \
 curl && \
rm -rf /var/cache/apk/*
# RUN curl -sSL https://install.pi-hole.net | bash

CMD curl -sSL https://install.pi-hole.net | bash
