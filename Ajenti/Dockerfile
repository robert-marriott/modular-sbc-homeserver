###############################################################################
#
#           Ajenti is a server information application
#      docker run -d --restart=always -p 84:8000 test-ajenti
#
###############################################################################
FROM armhf/alpine
# FROM alpine

ENV AJENTI_HOME="/home/ajenti"

RUN mkdir ${AJENTI_HOME} && \
    # Add dependencies for webmin to work
    apk add --update \
            tar \
            bash \
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

RUN  pip install ajenti-panel \
                 ajenti.plugin.dashboard \
                 ajenti.plugin.settings \
                 ajenti.plugin.plugins \
                 ajenti.plugin.filemanager \
                 ajenti.plugin.notepad \
                 ajenti.plugin.packages \
                 ajenti.plugin.services \
                 ajenti.plugin.terminal

CMD ["ajenti-panel","--autologin","-v"]
