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
apt-get --allow-unauthenticated install openmediavault-keyring && \
apt-get update && \
apt-get --yes --force-yes --auto-remove --show-upgraded \
	# --no-install-recommends \
	# --option Dpkg::Options::="--force-confdef" \
	# --option DPkg::Options::="--force-confold" \
	install postfix openmediavault

  # Initialize the system and database.
CMD omv-initsystem
