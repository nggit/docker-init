# openrc-alpine
Alpine Linux with openrc as PID 1, with an additional OpenSSH service.

## Build
```
docker-compose build --no-cache
```

## Run
```
docker-compose up
```

or run in the background:
```
docker-compose up -d
```

## Change the root password
```
docker exec -it openrc_alpine_10022 passwd
```

## Enter the console
```
docker attach openrc_alpine_10022
```
