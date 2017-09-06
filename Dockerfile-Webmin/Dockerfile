###############################################################################
#
# Webmin is a server information application
#
###############################################################################

# FROM hypriot/rpi-alpine-scratch
FROM alpine

ENV  DOWNLOAD_URL="http://prdownloads.sourceforge.net/webadmin/webmin-1.850.tar.gz" \
     WEBMIN_HOME="/home/webmin"

RUN mkdir ${WEBMIN_HOME} && \
    # Add dependencies for webmin to work
    apk add --update \
            tar \
            bash \
            perl \
            jpeg \
            wget && \
    rm -rf /var/cache/apk/* && \
    # Download and unpack webmin
    wget --no-check-certificate ${DOWNLOAD_URL} && \
    tar -xvzf webmin* -C ${WEBMIN_HOME} && \
    rm webmin*

CMD ["/bin/bash"]
