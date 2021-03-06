FROM debian:jessie

RUN apt-get -y update \
 && apt-get install -y wget lsb-release gnupg \
 && apt-get clean \
 && rm -rf /var/lib/apt/lists

# Avoid warning during packet installations
ENV DEBIAN_FRONTEND noninteractive

# Install the release key
# Set the RozoFS repository to access RozoFS packages
# Install RozoFS manager (optionally) required for all nodes
RUN wget -O - http://dl.rozofs.org/deb/devel@rozofs.com.gpg.key | apt-key add - \
 && echo deb  http://dl.rozofs.org/deb/master $(lsb_release -sc) main | tee /etc/apt/sources.list.d/rozofs.list \
 && echo 'APT::Install-Recommends "0";' > /etc/apt/apt.conf.d/01norecommend \
 && echo 'APT::Install-Suggests "0";' >> /etc/apt/apt.conf.d/01norecommend \
 && echo "#!/bin/sh\nexit 0" > /usr/sbin/policy-rc.d \
 && apt-get -y update \
 && apt-get install -y rozofs-manager* rozofs-* busybox inotify-tools \
 && apt-get clean \
 && rm -rf /var/lib/apt/lists

COPY rozofs /
CMD ["/rozofs"]
