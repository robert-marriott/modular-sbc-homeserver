# Using hypriot alpine scratch image because they know what they are doing, and
# this is an arm copatible image at about 3mb
FROM hypriot/rpi-alpine-scratch

RUN apk update && \
apk upgrade && \
apk add bash && \
rm -rf /var/cache/apk/*


CMD ["/bin/bash"]
