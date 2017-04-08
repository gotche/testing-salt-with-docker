#
# Salt Stack Salt Master Container
#

FROM debian:jessie
MAINTAINER Jose Martin <j.martin.bejarano@gmail.com>

# Update System
RUN apt-get update && apt-get upgrade -y -o DPkg::Options::=--force-confold

# dependencies
RUN apt-get install -y curl 

# Install salt
RUN curl -o bootstrap_salt.sh -L https://bootstrap.saltstack.com
RUN sh bootstrap_salt.sh -M -N -X

# Volumes
VOLUME ['/etc/salt/master', '/srv/salt', '/srv/pillar', '/etc/salt/pki', '/var/cache/salt/master']

# make sure this directory exists
RUN mkdir -p /var/run/salt/master

# Add Run File
ADD run.sh /usr/local/bin/run.sh
RUN chmod +x /usr/local/bin/run.sh

# Ports
EXPOSE 4505 4506

# Run Command
CMD "/usr/local/bin/run.sh"
