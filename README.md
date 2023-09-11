# systemd-debian
Debian image with a focus on running [systemd](https://systemd.io/) as PID 1.

## Supported tags
 - `bookworm`, `latest`
 - `bullseye`
 - `buster`

## How-to
1. Preparation

This step is only required for non-systemd host machines. Otherwise, skip this step.

```
sudo mkdir -p /sys/fs/cgroup/systemd
sudo mount -t cgroup -o none,name=systemd cgroup /sys/fs/cgroup/systemd
```

2. Create the container

`docker create -it --name systemd_debian --tmpfs /run --tmpfs /run/lock -v /sys/fs/cgroup:/sys/fs/cgroup:ro nggit/systemd-debian:bookworm`

3. Start the container

`docker start systemd_debian`

4. Set the root password

`docker exec -it systemd_debian passwd`

5. Enter the container

`docker attach systemd_debian`

Press "Enter" again if the login prompt does not appear immediately.

You can enter the container using `docker exec` as well. With the difference that the command you run will not be under the systemd process (PID 1).

## License
MIT
