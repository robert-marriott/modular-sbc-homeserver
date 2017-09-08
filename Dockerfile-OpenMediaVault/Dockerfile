###############################################################################
#
#           OpenMediaVault is a multifaceted NAS server software.
#
###############################################################################
FROM arm32v7/debian:jessie-slim

EXPOSE 80 443

RUN \
printf "deb http://packages.openmediavault.org/public arrakis main" > /etc/apt/sources.list.d/openmediavault.list && \
apt-get update && \
apt-get install -y aptitude && \
apt-get --allow-unauthenticated install openmediavault-keyring && \
apt-get update

RUN \
echo "deb http://packages.omv-extras.org/debian/ erasmus main" | sudo tee -a /etc/apt/sources.list.d/omv-extras-org-kralizec.list && \
sudo apt-get update && \
sudo apt-get install openmediavault-omvextrasorg -y --force-yes


RUN aptitude --assume-yes install openmediavault && \
rm -rf /var/lib/apt/lists/*
# postfix

  # Initialize the system and database.
CMD omv-initsystem
