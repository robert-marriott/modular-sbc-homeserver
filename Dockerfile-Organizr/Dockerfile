###############################################################################
#             Organizer is a multi server environment organizer.
#
# Organizr allows you to setup "Tabs" that will be loaded all in one webpage.
# You can then work on your server with ease.
#
# ** Based on an alpine ARM base image for raspberry pi and other SBC's
###############################################################################
FROM hypriot/rpi-alpine-scratch

RUN apk update && \
apk upgrade && \
apk add bash && \
rm -rf /var/cache/apk/*

RUN apk add wget && \
    apk add php7.0-sqlite && \
    apk add unzip

RUN wget https://github.com/causefx/Organizr/archive/master.zip && \
    unzip master.zip -d /path/to/web/ && \
    chown -R www-data:www-data /path/to/Organizr

CMD ["/bin/bash"]
