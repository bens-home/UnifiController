# UnifiController
A docker container that is the unifi network controller

Based on [this](https://github.com/linuxserver/docker-unifi-controller) official docker images

# Getting Started

```
docker-compose pull
docker-compose up -d
```

Now you can go to [https://localhost:8443](https://localhost:8443) to start your Unifi controller!

# Firewall rules
If you want to access the web interface elsewhere then you need to allow it through your server's firewall.

```
sudo ufw allow 8443/tcp comment "For Unifi controller web interface"

sudo ufw reload
```

# Useful commands

Shell access whilst the container is running: 
```
docker exec -it unifi-controller /bin/bash
```

To monitor the logs of the container in realtime:
```
docker logs -f unifi-controller
```
    
Get the container version number
```        
docker inspect -f '{{ index .Config.Labels "build_version" }}' unifi-controller
``` 

Get the image version number

```       
docker inspect -f '{{ index .Config.Labels "build_version" }}' lscr.io/linuxserver/unifi-controller:latest
```