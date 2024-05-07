FROM alpine:3.19

VOLUME ["/sys/fs/cgroup", "/run"]

# update
RUN apk update && apk upgrade

# install packages
RUN apk add openrc openssh

# clean up
RUN rm -rf /var/cache/apk/*

# unlock root account
RUN passwd -u root || true

# disable getty
RUN sed -i 's/^tty\([^:]*\):/#tty\1:/' /etc/inittab

# enable console
RUN echo 'console::respawn:/bin/login -p --' >> /etc/inittab

# configure sshd
# uncomment the following line to allow root login (insecure)
# RUN sed -i 's/^#*PermitRootLogin [-a-z]*/PermitRootLogin prohibit-password/' /etc/ssh/sshd_config
RUN sed -i 's/^#*AllowTcpForwarding [a-z]*/AllowTcpForwarding yes/' /etc/ssh/sshd_config; \
    sed -i 's/^#*GatewayPorts [a-z]*/GatewayPorts yes/' /etc/ssh/sshd_config; \
    sed -i 's/^#*ClientAliveInterval [0-9]*/ClientAliveInterval 120/' /etc/ssh/sshd_config; \
    sed -i 's/^#*ClientAliveCountMax [0-9]*/ClientAliveCountMax 720/' /etc/ssh/sshd_config

# fix hostname: sethostname: Operation not permitted
RUN sed -i 's/hostname $opts/#&/' /etc/init.d/hostname

# enable services at startup
RUN rc-update add sshd

EXPOSE 22

CMD ["/sbin/init"]
