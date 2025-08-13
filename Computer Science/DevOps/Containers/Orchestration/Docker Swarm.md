Swarms are provided by Docker Swarm, 
Swarms's official container orchestrator. It allows to create and manage containers across multiple machines.
swarm is a Docker native support for orchestrating cluster of docker engines.

A Swarm cluster of Docker hosts or nodes, is a highly available cluster of service that runs in swarm mode. The swarm cluster is run by what'd called managers and the work is done by worker node, which run the swarm service.

At a high level, Swarm takes multiple Docker engines running on different hosts and lets you use them together.

docker swarm has 2 types of nodes:
master (manager) and worker
the master controls the execution over the worker nodes

every swarm starts out with one managed node designated as the leader. 
Swarm is highly available thanks to its implementation of the Raft algorithm. 

Raft Algo: raft is a consensus algorithm designed to achieve fault tolerance in distributed systems.
the leader node is constantly checking in with its fellows manager

to inform a specific public IP:

`docker swarm init --advertise--addr IP`

`docker service create [service_name]`

to update a service
`docker service update [service-name] --replicas=[number of services]`
`docker service update ID --replicas 5`

to rollback
`docker service rollback ID`

To get Token at runtime
`docker swarm join-token manager` --> get the token for the manager

switch manager node in Docker
`docker node update --role manager [node_name]`

To add a machine to the cluster:
`docker swarm join --token [TOKEN]`

create a service with replicas
`docker service create --replicas [No] [image] [command]`
`docker service create --replicas 10 alpine ping www.google.com`

visualizer --> tool that can provide a graphical representation of the Docker Swarm cluster. 

execute compose file as Stack
`docker stack deploy -c docker-compose.yml visualizer`

file example
>[!example] Example - visualizer
>```yaml
>services:
>  visualizer:
>    image: dockersamples/visualizer:stable
>    container_image: swarm-visualizer
>    ports:
>      - "8090:8080"
>    volumes:
>      - "/var/run/docker.sock:/var/run/docker.sock" 
>    ports:
>      placement:
>        constraints:
>          - node.role == manager
>```

networks
docker swarm overlay the overlay network driver, creates a container network that spans multiple nodes

The goal of an overlay network is to make container running on multiple machines, and potentially multiple networks, appear as if they are on a single network. 

when the user initialize a swarm or join a Docker host to an existing swarm, two networks are created on the docker host:
- ingress --> overlay network, which handles control and data traffic related to swarm services
- bridge --> called docker_gwbridge, connects the individual Docker node to the other node participating the swarm

>[!note]
>If Swarm service is not connected with user defined Overlay Network, it connect to ingress network.

Rules for overlay network:
- open the TCP port 2377 for cluster management communications
- open TCP and UDP port 7946 for communication among nodes
- open UDP port 4789 for overlay network traffic

Obs: before create an overlay network, docker swarm must be initialized on Node or join it to an existing swarm.

>[!Example] Example - Postgres Service
>```shell
>docker service create --name postgres --network my_network -e POSTGRES_PASSWORD=mypas postgres
>```

