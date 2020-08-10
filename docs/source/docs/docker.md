# Docker
## How do I enable the remote API for dockerd

```
DOCKER_HOST=ssh://USER@HOST
```
OR 

https://success.docker.com/article/how-do-i-enable-the-remote-api-for-dockerd

1. Create a file at /etc/systemd/system/docker.service.d/startup_options.conf with the below contents:

```
# /etc/systemd/system/docker.service.d/override.conf
[Service]
ExecStart=
ExecStart=/usr/bin/dockerd -H fd:// -H tcp://0.0.0.0:2376
```

Note: The -H flag binds dockerd to a listening socket, either a Unix socket or a TCP port. You can specify multiple -H flags to bind to multiple sockets/ports. The default -H fd:// uses systemd's socket activation feature to refer to /lib/systemd/system/docker.socket.

2. Reload the unit files:

$ sudo systemctl daemon-reload

3. Restart the docker daemon with new startup options:

$ sudo systemctl restart docker.service

Ensure that anyone that has access to the TCP listening socket is a trusted user since access to the docker daemon is root-equivalent.

## Change owner for mounting folder
### docker-compose 
```
$ docker-compose exec SERVICE_NAME id
uid=100(www-data) gid=101(www-data) groups=101(www-data)
$ chown -R 100 ./
```
### docker
```
$ docker exec DOCKER_CONTAINER_ID id
uid=100(www-data) gid=101(www-data) groups=101(www-data)
$ chown -R 100 ./
```


