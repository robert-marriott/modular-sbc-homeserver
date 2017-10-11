
###############################################################################
# COPS is a web based ebook server with reader software. It can be used to
# distribute and read a collection of ebooks either with the web client, or an
# ODPS reader software.
###############################################################################
# FROM armhf/alpine:edge
FROM alpine:edge

#---------------------------- Base with S6 Overlay ----------------------------#
# set version for s6 overlay
ARG OVERLAY_VERSION="v1.19.1.1"
ARG OVERLAY_ARCH="amd64"

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

# ENTRYPOINT ["/init"]

#---------------------------- Base with S6 Overlay ----------------------------#
# install build packages
RUN \
 apk add --no-cache --virtual=build-dependencies \
	curl \
	tar && \

# install runtime packages
 apk add --no-cache \
	php7-dom \
	php7-gd \
	php7-intl \
	php7-mbstring \
	php7-opcache \
	php7-openssl \
	php7-phar \
	php7-pdo_sqlite \
	php7-zip \
	php7-zlib && \

# install composer
 ln -sf /usr/bin/php7 /usr/bin/php && \
 curl \
    -sS https://getcomposer.org/installer \
    | php -- --install-dir=/usr/bin --filename=composer && \
 composer \
	global require "fxp/composer-asset-plugin:~1.1" && \

# install cops
 COPS_VER=$(curl -sX GET "https://api.github.com/repos/seblucas/cops/releases/latest" \
	| awk '/tag_name/{print $4;exit}' FS='[""]') && \
 curl -o \
 /tmp/cops.tar.gz -L \
	"https://github.com/seblucas/cops/archive/${COPS_VER}.tar.gz" && \
 mkdir -p \
	/usr/share/webapps/cops && \
 tar xf /tmp/cops.tar.gz -C \
	/usr/share/webapps/cops --strip-components=1 && \
 cd /usr/share/webapps/cops && \
 composer \
	install --no-dev --optimize-autoloader && \

# cleanup
 apk del --purge \
	build-dependencies && \
 rm -rf \
	/root/.composer \
	/tmp/*

# add local files
COPY root/ /

# ports and volumes
EXPOSE 80
VOLUME /config /books
