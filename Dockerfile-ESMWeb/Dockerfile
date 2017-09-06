###############################################################################
#
#               ESM'Web is a server information application
#
###############################################################################

# FROM hypriot/rpi-alpine-scratch
FROM alpine

ENV  DOWNLOAD_URL="https://www.ezservermonitor.com/esm-web/downloads/version/2.5" \
     ESMWEB_HOME="/home/webmin"

RUN mkdir ${ESMWEB_HOME} && \
    # Add dependencies for ESM'Web to work
    apk add --update \
            unzip \
            bash \
            php \
            lighttpd \
            wget && \
    rm -rf /var/cache/apk/* && \
    # Download and unpack ESM'Web
    wget --no-check-certificate ${DOWNLOAD_URL} && \
    unzip 2.5 -d ${ESMWEB_HOME} && \
    rm 2.5
# In progress, need to run the directory in lighttpd
# https://www.ezservermonitor.com/esm-web/documentation
# https://www.linode.com/docs/web-servers/lighttpd/use-lighttpd-web-server-on-ubuntu-16-04
CMD ["/bin/bash"]
