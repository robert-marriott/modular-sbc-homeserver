
###############################################################################
# Linux-Dash is a supposedly lightweight, simple webui for monitoring Linux
# system information. It runs on whatever arbitrary webserver.
###############################################################################
FROM hypriot/rpi-alpine-scratch

ENV AJENTI_HOME="/home/ajenti"

RUN mkdir ${AJENTI_HOME} && \
    # Add dependencies for webmin to work
    apk add --update \
            tar \
            bash \
apache2 \
apache2-utils \
curl \
php5 \
php5-curl \
php5-json \
git \

            python-dev \
            linux-headers \
            libxml2-dev \
            libxslt-dev \
            libffi-dev \
            openssl-dev \
            jpeg-dev \
            musl-dev \
            py-pip \
            gcc \
            curl && \
    rm -rf /var/cache/apk/*

git clone https://github.com/afaqurk/linux-dash.git


# CMD ["ajenti-panel","--autologin","-v"]
