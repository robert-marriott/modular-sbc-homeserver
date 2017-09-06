docker create \
--name=pydio \
-v /etc/localtime:/etc/localtime:ro \
-v /tmp/docker/pydio/config:/config \
-v /tmp/docker/pydio/config:/data \
-e PGID=911 -e PUID=911  \
-e TZ="New York" \
-p 85:443 \
linuxserver/pydio
