###############################################################################
# Linux-Dash is a supposedly lightweight, simple webui for monitoring Linux
# system information. It runs on whatever arbitrary webserver.
###############################################################################
FROM arm32v7/debian:jessie-slim

ENV HOME=/home/cockpit \
    COCKPIT_REPO="deb https://fedorapeople.org/groups/cockpit/debian unstable main"

# Expose the port used for the webUI
EXPOSE 9090

# Create system user for running cockpit
RUN adduser --system cockpit && \
    addgroup cockpit && \
    mkdir -p ${HOME}
        # Add basic build dependencies
RUN echo ${COCKPIT_REPO} | tee -a /etc/apt/sources.list && \
    apt-key adv --keyserver sks-keyservers.net --recv-keys F1BAA57C && \
    apt-get update && \
    apt-get upgrade -y && \
    apt-get install -y cockpit cockpit-dashboard && \
    rm -rf /var/lib/apt/lists/*

# RUN systemctl enable --now cockpit.socket

# # Switch to homeassistnat user for virtualenvironment and such
# USER cockpit

CMD systemctl enable --now cockpit.socket
