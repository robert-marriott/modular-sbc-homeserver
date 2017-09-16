###############################################################################
# Cockpit is a simple webui for monitoring Linux
# system information.r.
###############################################################################
FROM arm32v7/debian:jessie-slim
# FROM debian:jessie-slim

ENV HOME=/home/cockpit \
    COCKPIT_REPO="deb http://repo-cockpitproject.rhcloud.com/debian/ jessie main"

# Expose the port used for the webUI
EXPOSE 9090

# Create system user for running cockpit
RUN adduser --system cockpit && \
    addgroup cockpit && \
    mkdir -p ${HOME}

        # Add basic build dependencies
RUN echo ${COCKPIT_REPO} > /etc/apt/sources.list.d/cockpit.list && \
    apt-key adv --keyserver sks-keyservers.net --recv-keys 0D2A45C3F1BAA57C && \
    apt-key finger F1BAA57C && \
    apt-get update && \
    apt-get install cockpit cockpit-dashboard && \
    rm -rf /var/lib/apt/lists/*

# RUN systemctl enable --now cockpit.socket

# # Switch to homeassistnat user for virtualenvironment and such
# USER cockpit

# CMD systemctl enable --now cockpit.socket
