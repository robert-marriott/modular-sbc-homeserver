FROM hypriot/rpi-node

COPY StaticWelcomePage /public

RUN npm install http-server -g

CMD ["http-server -p 80"]
