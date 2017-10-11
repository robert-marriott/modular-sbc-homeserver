###############################################################################
# Adapted from linuxserver.io, a docker base image with alpine and s6 process
# manager. Small and efficient.
# Image will be named 'sbc-armf-base-alpine'
###############################################################################
FROM scratch

# This adds the root file system for alpine 3.6
ADD alpine-minirootfs-3.6.2-armhf.tar.gz /

# set version for s6 overlay
ARG OVERLAY_VERSION="v1.19.1.1"
ARG OVERLAY_ARCH="armhf"

# environment variables
ENV PS1="$(whoami)@$(hostname):$(pwd)$ " \
HOME="/root" \
TERM="xterm"

# install packages
RUN \
 apk add --no-cache --virtual=build-dependencies \
	curl \
	tar && \
 apk add --no-cache \
	bash \
	ca-certificates \
	coreutils \
	shadow \
	tzdata && \

# add s6 overlay
 curl -o \
 /tmp/s6-overlay.tar.gz -L \
	"https://github.com/just-containers/s6-overlay/releases/download/${OVERLAY_VERSION}/s6-overlay-${OVERLAY_ARCH}.tar.gz" && \
 tar xfz \
	/tmp/s6-overlay.tar.gz -C / && \

# create abc user
 groupmod -g 1000 users && \
 useradd -u 911 -U -d /config -s /bin/false abc && \
 usermod -G users abc && \

# make our folders
 mkdir -p \
	/app \
	/config \
	/defaults && \

# clean up
 apk del --purge \
	build-dependencies && \
 rm -rf \
	/tmp/*

# add local files
COPY root/ /

ENTRYPOINT ["/init"]
