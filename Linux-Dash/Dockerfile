
###############################################################################
# Linux-Dash is a supposedly lightweight, simple webui for monitoring Linux
# system information. It runs on whatever arbitrary webserver.
###############################################################################
FROM armhf/alpine:edge

# Add dependencies for Linux-Dash to work
RUN  apk update && apk upgrade && \
     apk add  bash \
              nodejs \
              nodejs-npm \
              git && \
    # clone git repo onto filesystem
    git clone https://github.com/afaqurk/linux-dash.git && \
    cd linux-dash/app/server && \
    # install node dependencies
    npm install --production && \
    apk del nodejs-npm && \
    apk del git && \
    rm -rf /var/cache/apk/* && \
# Create container unpriveleged base user and diretory structure
    adduser -s /bin/bash -u 1001 -G root -D default && \
    chown -R 1001:0 /linux-dash

EXPOSE 80 443

USER 1001

CMD node /linux-dash/app/server/index.js --port 8080
