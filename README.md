# Docker Swarm
To initialize docker swarm
$ docker swarm init --advertise-addr 10.0.12.3

O/P:
Swarm initialized: current node (xxdo1afkprfk2cxqye6h8kh5l) is now a manager.

To add a worker to this swarm, run the following command:

    docker swarm join \
    --token SWMTKN-1-685tex5di7ruhale4pjb011grpm36zdrfa0f3h09fd3s5bqhho-9jkux4mrezshe8ef0h37hqeuy \
    172.31.14.112:2377

To add a manager to this swarm, run 'docker swarm join-token manager' and follow the instructions.

To list docker nodes:
$ docker node ls
O/P:
ID                                                     HOSTNAME             STATUS             AVAILABILITY     MANAGER STATUS
xxdo1afkprfk2cxqye6h8kh5l *     node1                        Ready                 Active                      Leader
To leave Swarm:
$ docker swarm leave

To make the other node as Master:
$ docker swarm join-token manager
O/P:
To add a manager to this swarm, run the following command:
    docker swarm join \
    --token SWMTKN-1-2gxlg3lqbe24osxi8vhxiq6p64cxpar3g7ds83q1zqui447i6o-12zx8bkzuuk4scr9yjbc2xd50 \
    10.0.12.3:2377
To make the other node as worker:
Copy the O/P of master docker init
Exg.
docker swarm join \
    --token SWMTKN-1-2gxlg3lqbe24osxi8vhxiq6p64cxpar3g7ds83q1zqui447i6o-bao4b66lekvne2gqdye4weps8 \
    10.0.12.3:2377
