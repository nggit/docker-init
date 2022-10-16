# Copyright (c) 2022 nggit.
#
FROM debian:sid

VOLUME ["/sys/fs/cgroup", "/run", "/run/lock"]

# update system & install packages
RUN apt-get update && apt-get -y upgrade; \
    apt-get -y install systemd-sysv

# clean up
RUN apt-get clean; \
    rm -rf /etc/machine-id /var/lib/dbus/machine-id /var/lib/apt/lists/* /tmp/* /var/tmp/*; \
    find /var/log -name "*.log" -type f -delete

# tweaks
RUN sed -i 's/^#*ReadKMsg=[a-z]*/ReadKMsg=no/' /etc/systemd/journald.conf; \
    systemctl disable getty@tty1.service

# allow systemd (and other programs) to identify that it is executed within a container
# https://systemd.io/CONTAINER_INTERFACE/
ENV container docker

STOPSIGNAL 37

ENTRYPOINT ["/usr/bin/env", "--"]
CMD ["sh", "-c", "mount -o remount,ro /sys 2> /dev/null; systemd-machine-id-setup; exec /sbin/init"]
