# UnifiController
A docker container that is the unifi network controller

Based on [this](https://github.com/linuxserver/docker-unifi-controller) official docker images

# Getting Started

```
docker-compose pull
docker-compose up -d
```

Now you can go to [https://<IP of your server>:8443](https://localhost:8443) to start your Unifi controller!

Set the "Override inform host with controller hostname/IP" checkbox to true. 
In the text box next to it, set the hostname the IP of your server such as `192.168.1.X`

# Firewall rules
If you want to access the web interface elsewhere then you need to allow it through your server's firewall.

The Unifi controller needs a bunch of ports for it's auto-discovery of devices, so you will
need to make sure that you expose them through your host machines firewall. Here are some UFW
rules you can add to make that work! 

```
sudo ufw allow 8443 comment "For Unifi web admin port"
sudo ufw allow 3478/udp comment "For Unifi STUN port"
sudo ufw allow 10001/udp comment "Required for AP discovery"
sudo ufw allow 1900/udp comment "Unfi: Required for Make controller discoverable on L2 network option"
sudo ufw allow 8843 comment "Unifi: Unifi guest portal HTTPS redirect port"
sudo ufw allow 8880 comment "Unfi: Unifi guest portal HTTP redirect port"
sudo ufw allow 6789 comment "Unfi: For mobile throughput test"
sudo ufw allow 5514/udp comment "Unfi: Remote syslog port"

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