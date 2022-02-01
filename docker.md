# docker

## Publish port

```bash
docker run -p BIND_IP:BIND_PORT:CONTAINER_PORT
```

Has the host binding first (before the colon `:`) and the container port second.

https://docs.docker.com/engine/reference/commandline/run/#publish-or-expose-port--p---expose

## Quick FTP

https://github.com/delfer/docker-alpine-ftp-server

But don't use `ftp` as username, had some failure last time I tried.

## Copy file to / from container

```bash
docker cp mytestfile1.txt mycontainer1:/usr/src/app/mytestfile1.txt
docker cp src_file_with_path  container_name:/destination_path
```

## Start shell in container

```bash
docker exec -it <container-id> /bin/bash
```

