#
# Salt Stack Salt minion Container
#

FROM debian:jessie
MAINTAINER Jose Martin <j.martin.bejarano@gmail.com>

RUN echo "deb http://repo.saltstack.com/apt/debian/8/amd64/latest jessie main" >> /etc/apt/sources.list.d/saltstack.list
RUN gpg --keyserver pgpkeys.mit.edu --recv-key 0E08A149DE57BFBE
RUN gpg -a --export 0E08A149DE57BFBE | apt-key add -
RUN apt-get update && apt-get install -y --force-yes salt-common salt-minion && apt-get clean &&  rm -rf /var/lib/apt/lists/*

ADD etc/minion /etc/salt/minion
ADD etc/minion_id /etc/salt/minion_id

# Locales
ENV DEBIAN_FRONTEND noninteractive
RUN apt-get update && apt-get install -y locales && apt-get clean
RUN sed -i -e 's/# en_US.UTF-8 UTF-8/en_US.UTF-8 UTF-8/' /etc/locale.gen && \
    echo 'LANG="en_US.UTF-8"'>/etc/default/locale && \
    dpkg-reconfigure --frontend=noninteractive locales && \
    update-locale LANG=en_US.UTF-8

ENV LANG en_US.UTF-8  

# Sysmtemd peculiarities
RUN cd /lib/systemd/system/sysinit.target.wants/; ls | grep -v systemd-tmpfiles-setup | xargs rm -f $1 \
rm -f /lib/systemd/system/multi-user.target.wants/*;\
rm -f /etc/systemd/system/*.wants/*;\
rm -f /lib/systemd/system/local-fs.target.wants/*; \
rm -f /lib/systemd/system/sockets.target.wants/*udev*; \
rm -f /lib/systemd/system/sockets.target.wants/*initctl*; \
rm -f /lib/systemd/system/basic.target.wants/*;\
rm -f /lib/systemd/system/anaconda.target.wants/*; \
rm -f /lib/systemd/system/plymouth*; \
rm -f /lib/systemd/system/systemd-update-utmp*;

RUN systemctl set-default multi-user.target
ENV init /lib/systemd/systemd
RUN systemctl enable salt-minion
VOLUME [ "/sys/fs/cgroup" ]
ENTRYPOINT ["/lib/systemd/systemd"]
