# Docker Swarm ![](/dockerswarm.gif)

Install CS Docker Engine by logging in into each host using ssh, 
```
curl -SLf https://packages.docker.com/1.13/install.sh  | sh
```
Service: Let us a single service called *web* that runs the latest nginx:
```
docker service create -p 80:80 --name web nginx:latest
docker service ls
```
Now open the machine address in your browser : Any node , Next let's inspect the service : `docker service inspect web`
That's lots of info! Now, let's scale the service: `docker service scale web=15` and Docker has spread the 15 services evenly over all of the nodes
Run `docker service ps web` to see the services divided and running across nodes
You can also drain a particular node, that will remove all services from that node and the services will automatically be rescheduled on other nodes.
`docker node update --availability drain <node>` then run `docker service ps web`
Run `docker node ls` and you can check out the nodes and see that 'node' is still active but drained `docker service ps web`
Now bring 'node' back online and show it's new availability `docker node update --availability active <node>` and inspect the node using `docker node inspect worker1 --pretty`
Install Universal Control Plane
- Docker Universal Control Plane (UCP) allows managing from a centralized place your images, applications, networks, and other computing resources
```
docker run --rm -it --name ucp \
  -v /var/run/docker.sock:/var/run/docker.sock \
  docker/ucp:2.1.1 install \
  --host-address <node-ip-address> \
  --interactive
```
where <node-ip-address> is the IP address of the host
License your installation
To initialize docker swarm `docker swarm init --advertise-addr 10.0.12.3`
The Output will be as.
```
Swarm initialized: current node (xxdo1afkprfk2cxqye6h8kh5l) is now a manager.

To add a worker to this swarm, run the following command:

    docker swarm join \
    --token SWMTKN-1-685tex5di7ruhale4pjb011grpm36zdrfa0f3h09fd3s5bqhho-9jkux4mrezshe8ef0h37hqeuy \
    172.31.14.112:2377

To add a manager to this swarm, run 'docker swarm join-token manager' and follow the instructions.
```

To list docker nodes `docker node ls`

```
ID                                                     HOSTNAME             STATUS             AVAILABILITY     MANAGER STATUS
xxdo1afkprfk2cxqye6h8kh5l *     node1                        Ready                 Active                      Leader
```
To leave the node from Swarm `docker swarm leave`
To make the other node as Master `docker swarm join-token manager`

```
To add a manager to this swarm, run the following command:
    docker swarm join \
    --token SWMTKN-1-2gxlg3lqbe24osxi8vhxiq6p64cxpar3g7ds83q1zqui447i6o-12zx8bkzuuk4scr9yjbc2xd50 \
    10.0.12.3:2377
```
To make the other node as worker:
Copy the O/P of master docker init
Exg.
docker swarm join \
    --token SWMTKN-1-2gxlg3lqbe24osxi8vhxiq6p64cxpar3g7ds83q1zqui447i6o-bao4b66lekvne2gqdye4weps8 \
    10.0.12.3:2377
