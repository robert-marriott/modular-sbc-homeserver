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

docker run -d --name hass -p 8123:8123 --net=host -v /etc/localtime:/etc/localtime:ro -v haas-data:/config lroguet/rpi-home-assistant:latest

OVPN_DATA="ovpn-data"
docker volume create --name $OVPN_DATA

docker run -v $OVPN_DATA:/etc/openvpn --rm giggio/openvpn-arm ovpn_genconfig -u udp://108.56.166.154
docker run -v $OVPN_DATA:/etc/openvpn --rm -it giggio/openvpn-arm ovpn_initpki nopass
docker run -v $OVPN_DATA:/etc/openvpn -d --name openvpn -p 1194:1194/udp --cap-add=NET_ADMIN giggio/openvpn-arm
docker run -v $OVPN_DATA:/etc/openvpn --rm -it giggio/openvpn-arm easyrsa build-client-full robert nopass
docker run -v $OVPN_DATA:/etc/openvpn --rm giggio/openvpn-arm ovpn_getclient robert > robert.ovpn
