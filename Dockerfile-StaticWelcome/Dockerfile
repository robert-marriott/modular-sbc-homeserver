FROM hypriot/rpi-node

COPY StaticWelcomePage /public

RUN npm install http-server -g

CMD ["/bin/bash http-server -p 80"]
