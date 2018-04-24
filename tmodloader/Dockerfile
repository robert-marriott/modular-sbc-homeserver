FROM alpine:edge

ENV SERVER_VERSION="1353" \
    OFFICIAL_URL="http://terraria.org/server" \
    OFFICIAL_ZIP="terraria-server-1353.zip" \
    MODLOADER_URL="https://github.com/blushiemagic/tModLoader/releases/download/v0.10.1.3" \
    MODLOADER_ZIP="tModLoader.Linux.v0.10.1.3.zip"

RUN apk update \
    && apk upgrade && \
    && apk add \
     bash \
     wget \
    && rm -rf /var/cache/apk/* \
  # Install necessary server files
    && mkdir terraria \
    && cd terraria \
    && wget $OFFICIAL_URL/$OFFICIAL_ZIP \
    && unzip $OFFICIAL_ZIP \
    && rm -rf ./$SERVER_VERSION/Mac ./$SERVER_VERSION/Windows \
    && mv ./$SERVER_VERSION/Linux/* . \
    && wget $MODLOADER_URL/$MODLOADER_ZIP \
    && unzip $MODLOADER_ZIP \
    && rm *.zip \
    && chmod +x tModLoaderServer \
  # Clean up unneeded alpine packages
    && apk delete wget

# Allow for external data
# VOLUME ["/terraria/world", "/tshock/ServerPlugins"]

# Set working directory to server
WORKDIR /terraria

# run the server
ENTRYPOINT ["./tModLoader","-steam","-autocreate 1"]
