This is my build of homeassistant.io, as the other images for ARM processors
were not functioning.

Create a volume for configuration:
```
docker volume create --name hass-data
```

Create the running pod
```
docker run -d --name="home-assistant" --restart=always -p 8123:8123 -v hass-data:/config -v /etc/localtime:/etc/localtime:ro imightbebob/home-assistant-arm7
```
