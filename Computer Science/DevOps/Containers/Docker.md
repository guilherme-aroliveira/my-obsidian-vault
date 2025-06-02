Available since 2013, Docker is an open platform (engine) written in Go, that allows to develop, deploy, test and run applications as containers. It uses Linux kernel's features to deliver functionality.

Docker isolates applications from infrastructure, including the hardware, operating systems and the container runtime. It uses the namespaces technology to provide an isolated workspace called "container" (containers are isolated from each other).

Docker creates a set of namespaces for every container and each aspect runs in a separate namespace with access limited to that namespace.

>[!info]
><span style="color: #d65d0e">namespaces</span> is a <strong>feature of the Linux kernel</strong> that allows to provide complete network isolation to different processes on the system. It's similar in concept to what a <span style="color: #d65d0e">Hypervisor</span> does to provide the virtual resources to the Virtual Machine.

Namespaces keep containers isolated until docker administrator allows containers to communicate over docker virtual network on the same host. 

<span style="color:#98971a">Process ID namespaces</span> <span style="color: #3588E9">--></span> namespace isolation technique

The processes running inside the container are in fact processes running on the underlying host. With process ID namespaces, each process can have multiple process IDs associated with it.

By default there is no restriction as to how much of a resource a container can use, and hence a container may end up utilizing all of the resources on the underlying host.

Docker primarily uses <span style="color: #d65d0e">cgroups</span> (control groups) to restrict the amount of hardware resources allocated to each container <span style="color: #3588E9">--></span> can be done by providing the `--cpus` option to the Docker run command. 

>[!example] cgroups - example
>```shell
>docker run --cpus=.5ubuntu
>```
>Ensure that the container does not take up more than 50% of the host CPU at any given time
>```shell
>docker run --memory=100m ubuntu
>```
>The same goes with memory

Docker requires that virtualization to be enabled in the Bios, <span style="color: #d65d0e">VT-X</span> or <span style="color: #d65d0e">AMD-V</span>.

>[!note]
> The main purpose of Docker is to package and containerized applications and to ship them and to run them anywhere any time as many times is needed.
##### <span style="color: #d65d0e">Docker Engine</span>

Docker consist of multiple tools that are grouped together like <span style="color:#98971a">Docker CLI</span>, <span style="color:#98971a">Docker API</span>, the build tools for building images.

The <span style="color: #d65d0e">Docker Engine</span> which is the <strong style="color: #d79921">heart of Docker</strong>, is comprised of runtime and packing tools, and is required to be installed on the host that runs Docker. It's <strong>designed as client-server application</strong>, and it has these components: <span style="color:#98971a">Docker CLI</span> (docker client), <span style="color:#98971a">Dockerd</span> (docker daemon), <span style="color:#98971a">REST APIs</span>.

<span style="color:#98971a">Dockerd</span> <span style="color: #3588E9">--></span> it's the docker host server itself. The daemon listens for Docker API request or commands such as "docker run" and processes those commands. The daemon, is responsible for: build, run and distributes containers to the registry. Docker host includes and manages: images, containers, namespaces, networks, storage, plugins and add-on.

<span style="color:#98971a">Docker CLI</span> <span style="color: #3588E9">--></span> send instructions/commands to the Docker host server via command line interface (CLI) or through REST APIs. The Docker CLI can be used to communicate with local and remote host. The Docker CLI and the <span style="color:#98971a">Dockerd</span> can run on the same system or connect the client to a remote docker daemon.

To use Docker CLI to work with remote docker engine, simply use `-h` option on the Docker command and specify the remote Docker engine address and a port.

>[!example] Docker CLI
>```shell
>docker -H=10.123.2.1:2375 run nginx
>```
>`docker -H=[remote-docer-engine]:[port]`

<span style="color: #3588E9">--></span> <span style="color:#98971a">docker daemon</span> can also communicate with other daemons to manage Docker services.
##### <span style="color: #d79921">Docker Architecture</span>

Docker is based on client-server architecture which provides a complete application environment. Docker components includes the client, the host, and the registry.

Docker hosts are also called nodes, and they also include and manage: Images, Containers, Namespaces, Networks, Storage, Plugins and add-ons.

Docker stores and distributes images in a <span style="color:#98971a">Registry</span> (stateless and high scalable application) <span style="color: #3588E9">--></span> the access is public or private, such as <span style="color:#98971a">Docker Hub</span> (default public registry which is cloud-based), Private (implemented for security).

>[!info]
>Registry locations are either hosted on thirds party providers (such as IBM cloud Container registry) or self-hosted in private data center or in the cloud.
>
> registry access: <span style="color:#689d6a">PUSH</span> <span style="color: #3588E9">--></span> [<span style="color:#98971a"> registry </span>] <span style="color: #3588E9"> --> </span> <span style="color:#689d6a">PULL</span>
> <strong style="color: #d65d0e">image:</strong> <code style="color:#689d6a">[Registry]/[User/Account/Image/Repository]</code> <span style="color: #3588E9">--></span> <code style="color:#689d6a">docker.io/library/nginx</code>

<span style="color: #3588E9">--></span> The <span style="color: #d65d0e">Docker Registry</span> is itself another application, and it's available as a Docker image.

To run a container using an image from a private registry, first log in to the private registry
- `docker login private-registry.io`

>[!example] <strong style="color: #b16286">Deploy</strong> private registry:
>```shell
>docker run -d -p 5000:5000 --name registry registry:2
>
># tag the image with the private registry URL
>docker image tag my-image localhost:500/my-image
>
># push the image to the local private registry
>docker push localhost:5000/my-image
>
># pull the image from the localhost
>docker pull localhost:5000/my-image
>
># pull the image using the IP
>docker pull 192.168.56.100:5000/my-image
>```

The two main Docker components, Client and Server (host), communicate via socket, that can be a network socket where the Client is running on one computer and the Server in another computer in a <span style="color: #d65d0e">Cloud Provider</span>, or they can be running on same hardware, with the Server in a virtual machine, which a common case.

<span style="color: #3588E9">--></span> When the Client and the Server are running on the same computer, they connect through a special file called socket. The Client can run even run inside Docker itself.

Docker also uses "copy-on-write" file systems to build images.

<span style="color:#98971a">copy-on-write</span> <span style="color: #3588E9">--></span> Docker takes each layer, split them and make them into `gzip` files and ships them over the network separately, and the receiving end of that connection (running Docker server) receives all those layers separately and then puts them together using the file system.

<span style="color: #d65d0e">Docker Enterprise</span> provides the Universal Control Plane (UCP) and <span style="color: #d65d0e">Docker Trusted Registry</span> (DTR). Docker EE contains not only the container runtime but also <span style="color: #d65d0e">Docker Swarm</span> orchestration, docker volumes, networking and security.

UCP include centralized policy management for all containers centralized role-based access control, user management, application cluster management and the ability to organize the container as services and stacks.

DTR is an on-site, on-premises registry for centralized storage for all the containers images. It can also include secure image scanning and continuous monitoring of the images in the registry.
##### <span style="color: #d79921">Docker Objects</span>
###### <span style="color:#98971a">Image</span>

A Docker image is a read-only template with instructions for creating Docker container.

<span style="color:#98971a">Docker images</span> consist on multiple layers, which are <strong>Read-Only</strong>, and each of these layers has an unique ID.

<span style="color: #d65d0e">Layers</span> are saved on disk only once and can be shared between images, which saves disk space and network bandwidth.

Each <span style="color: #d65d0e">layer</span> is only a set of differences from the layer before it, the layers are stacked on top of each other. When an image is run as a container a new <span style="color: #d65d0e">writable layer</span> (container layer) is added, which allows to make changes to the container.

Multiple containers are typically based on the same image, called <span style="color: #d65d0e">base image</span>. Changes made to the base image are actually stored in a new layer and don't the base layer.

All changes made to the running container, are written to the container layer. But the files won't be persistent after the container is deleted. To write data in the writable layer of the container, Docker uses <span style="color: #d65d0e">storage drivers</span>.

Naming a Docker image: 
- <code style="color:#689d6a">[registry]/[repository]:[tag]</code> <span style="color: #3588E9">--></span> <code style="color:#689d6a">docker.io/ubuntu:18.04</code>

<span style="color: #d65d0e">Tags</span> are essentially <strong>aliases</strong>, an image can have multiple tags, but all points to the same source image. The tag <code style="color:#689d6a">latest</code> is a tag associated to the latest version of a software, which is governed by the authors of that software.

>[!note]
> Each version of the software can have multiple short and long tags associated with it

A <span style="color: #d65d0e">Docker repository</span> within a registry is a collection of related Docker images with the same name but different tags. Each image is stored as a tag that can refer to different variations of an image.

>[!note]
>many companies choose to run their own registry within their own company to ensure that their data stays safe and private

<span style="color: #d65d0e">Dangling images</span> are <strong>layers that have no relationship</strong> to any tagged images.

To modify the <span style="color: #d65d0e">entrypoint</span> during runtime: 
- <code style="color:#689d6a">docker run --entrypoint sleep2.0 ubuntu-sleeper 10</code>
###### <span style="color:#98971a">Container</span>

A container is a runnable instance of an image, it encapsulates everything an application needs to run.

Can be created, stopped, started or deleted using the Docker API or CLI.

Can connect to multiple networks, attach storage to the container, or create a new image based on its current state.

Is well isolated from other containers an its host machine.

Containers are independent of the storage containers. Depending on the storage layer, in some cases it may run out of layers. Some storage have a limited number of layers.

Each container automatically gets a random ID and name created for it by Docker.

The Container ID uniquely identifies the container, it's used to refer to a certain container. When a container is started, if Docker doesn't return the Docker ID, then something is wrong. If there isn't an image on the machine, Docker will download the image.

All Docker container are nothing more than a process, looked from the perspective of the operating systems.

In Docker, the container starts with an init process and vanishes when this process exits.

To keep a long running container, its necessary to specify what the <span style="color: #d65d0e">Process ID 1</span> is. If that process is gone, the container will stop.
###### <span style="color:#98971a">Dockerfile</span>

A Dockerfile is a text file that contains instructions needed to create an image, it can be created using any editor, from the console or terminal.

Each docker instruction on a Dockerfile creates a new layer in the image.

>[!example]
>```dockerfile
># Pull basde image
>FROM ubuntu:14:04
>
># Install
>RUN \
>sed -i '' \
>apt-get update && \
>apt-get -y upgrade && \
>apt-get install -y build-essential && \
>apt-get install -y software-properties-common && \
>apt-get install -y byobu curl git htop man unzip vim wget
>
># Add files
>ADD root/.bashrc /root/.bashrc
>ADD root/.gitconfig /root/.gitconfig
>ADD root/.scripts /root/.scripts
>
># Set environment variables
>ENV HOME /root
>
># Define working directory
>WORKDIR /root
>
># Define default command
>CMD ["bash"]
>```

Dockerfile elements
- <code style="color: #689d6a">FROM</code> <span style="color: #3588E9">--></span> it defines the base image
- <code style="color: #689d6a">RUN</code> <span style="color: #3588E9">--></span> executes arbitrary commands
- <code style="color: #689d6a">CMD</code> <span style="color: #3588E9">--></span> stands for command, it defines the program that will be run within the container when it starts.
	- Obs: should only have 1 command instructions.
	- Different ways of specifying commands:
		- Shell form: `command1 param1`
		- JSON array: `["command", "param1"]` <span style="color: #3588E9">--></span> Obs: the first element should be the executable
- <code style="color: #689d6a">ENTRYPOINT</code> <span style="color: #3588E9">--></span> similar to the CMD instruction, it can specify the program that will run when the container starts.

A Dockerfile is executed by the <code style="color:#689d6a">docker build</code> command

>[!example] docker build
>```shell
>docker build nginx
>```
>When Docker finishes running the Dockerfile, the resulting image will be on the <span style="color: #d65d0e">local registry</span>.

Each step of running a Dockerfile is cached, Docker skips lines that haven't changed since the last build.
###### <span style="color:#98971a">Network</span>

network are used for the isolated container communication.

When Docker is installed, it creates three networks automatically: Bridge, None, Host. Bridge is the default network a container gets attached to. docker run Uuntu --network=host --> to associate the container with any other network

The Bridge Network is a private internal network created by Docker on the host.

Another way to access the containers externally is to associate the container to the host network. This takes out any network isolation between the Docker host and the Docker container.

With the non network. The containers are not attached to any network and doesn't have any access to the external network or other containers. They run in an isolated network.

By default, Docker only creates one internal bridge network.

All containers attached to this network by default, and they get an internal IP address usually in the range 172.17.0.0 series. The containers can access each other using this internal IP if required

Every docker container gets an IP assigned by default, but it's an internal IP

<code style="color:#689d6a">docker run -p 8283:8080 nginx</code> <span style="color: #3588E9">--></span> traffic on port 8283 docker host will get routed to port 8080 inside the container

The same port can't be mapped on the Docker host more than once.

Meaning if you were to run a web server on Port 5000 in a web app container, it is automatically as accessible on the same port externally without requiring any port mapping as the web container uses the host's network. This would also mean that unlike before, you will now not be able to run multiple web containers on the same host on the same port as the ports are now common to all containers in the host network.

We could create our own internal network using the Command Docker network, create and specify the driver, which is bridge in this case and the subnet for that network, followed by the custom isolated network name run.

The docker network ls command to list all networks.
###### <span style="color:#98971a">Storage</span>

Docker uses volumes and bind mounts to persist data even after a container stops

Docker stores all its data by default on this location: `/var/lib/docker`

<code style="color:#689d6a">docker volume create</code> <span style="color: #3588E9">--></span> docker command to create a volume

>[!example] example - docker volume create
>```shell
>docker volume create d_volume
>```
>creates a folder called d_volume under the `/var/lib/docker/volumes` directory.

To persist data, it's necessary to mount a volume or map a directory outside the container on the docker host or host to a directory inside the container.

>[!example] mount volume
>```shell
># volume mouting
>docker run -v data_volume:/var/lib/mysql myql
>```
>A new container is created and mount the data volume into the /lib/mysql folder inside the container. All the data will now be stored in the external volume, and will remain even if the Docker container is deleted.
>
>The <code style="color:#689d6a">-v</code> option on the <code>docker run</code> command, Docker will automatically create a volume automatically.

The are two types of mounts:
- <span style="color:#98971a">volume mounting</span> <span style="color: #3588E9">--></span>  mounts a volume from the volumes directory
- <span style="color:#98971a">bind mounting</span> <span style="color: #3588E9">--></span> mounts a directory from any location on the Docker host

>[!example] bind mount
>```shell
>docker run -v /data/mysql:var/lib/mysql mysql
>```

>[!example] --mount option
>```shell
>docker run \ --mount type,source=/data/mysql,target=var/lib/mysql mysql
>```
>The source is the location on the host and the target is the location on the container.


Docker uses storage drivers to enable layered architecture. Some of the common storage drivers are: AUFS, ZFS, BTRFS, Device Mapper, Overlay, Overlay2. The selection of the storage driver depends on the underlying OS.

>[!info]
>Docker will choose the best storage driver available automatically based on the operating system.

How can I get my web server to access the database on the database container?

The right way to do it is to use the container name. All containers in a docker host can resolve each other with the name of the container. Docker has a built in DNS server that helps the containers to resolve each other using the container name.

How were the containers isolated within the host?
Docker uses network namespaces that creates a separate namespace for each container. It then uses virtual ethernet pairs to connect containers together.
##### <span style="color: #d79921">Docker Commands</span>

- To <strong style="color: #b16286">run/start</strong> a container from an image <span style="color: #3588E9">--></span> <code style="color:#689d6a">docker run nginx</code>   
	- <code style="color:#689d6a">docker run redis:40</code> <span style="color: #3588E9">--></span> specifying a tag
		- To <strong style="color: #b16286">list all</strong> running containers <span style="color: #3588E9">--></span> <code style="color:#689d6a">docker ps</code>
			- <code style="color:#689d6a">-a</code> option <span style="color: #3588E9">--></span> to list all containers
			- <code style="color:#689d6a">docker container ls</code> <span style="color: #3588E9">--></span> new syntax
	- <code style="color:#689d6a">-d</code> option <span style="color: #3588E9">--></span> for detach mode, it runs the container in the background mode
	- <code style="color:#689d6a">-i</code> option <span style="color: #3588E9">--></span> for interactive mode
	- <code style="color:#689d6a">-t</code> option <span style="color: #3588E9">--></span> for pseudo terminal
	- <code style="color:#689d6a">-p</code> <span style="color: #3588E9">--></span> for port mapping
		- Ex: <code style="color:#689d6a">docker run -p 8283:8080 nginx</code> 
	- <code style="color:#689d6a">-v</code> <span style="color: #3588E9">--></span> for volume mapping
	- <code style="color:#689d6a">-e</code> <span style="color: #3588E9">--></span> for environment variables
		- Ex: <code style="color:#689d6a">docker run -e APP_COLOR=pink webapp</code>
	- <code style="color:#689d6a">--link</code> <span style="color: #3588E9">--></span> option which can be used to link to containers together.
		- it creates an entry into the etc/hosts file on the voting app container, adding an entry with the host name redis with the internal IP of the redis container.
		- Ex: <code style="color:#689d6a">docker run -d --name=vote -p 500:80 --link redis:redis voting:app</code>
- To <strong style="color: #b16286">stop</strong> a container <span style="color: #3588E9">--></span> <code style="color:#689d6a">docker stop</code>
	- must provide either the container ID or the container name. Ex: <code style="color:#689d6a">docker stop silly_sammet</code>
- To <strong style="color: #b16286">remove</strong> a container permanently <span style="color: #3588E9">--></span> <code style="color:#689d6a">docker rm [id]</code>
	- must provide either the container ID or the container name
	- <code style="color:#689d6a">docker container rm [container_id]</code> <span style="color: #3588E9">--></span> new syntax
- To <strong style="color: #b16286">inspect</strong> a container <span style="color: #3588E9">--></span> <code style="color:#689d6a">docker inspect [name]</code>
	- it returns all details of a container in a JSON format
- To <strong style="color: #b16286">see the logs</strong> of a container <span style="color: #3588E9">--></span> <code style="color:#689d6a">docker logs [name]</code>
- To <strong style="color: #b16286">list all</strong> available images <span style="color: #3588E9">--></span> <code style="color:#689d6a">docker images</code>
	- <code style="color:#689d6a">docker image ls</code> <span style="color: #3588E9">--></span> new syntax
- To <strong style="color: #b16286">delete an image</strong> <span style="color: #3588E9">--></span> <code style="color:#689d6a">docker rmi [id]</code>
	- all dependent containers must be stopped or deleted
	- `docker image rm` --> new syntax
- To <strong style="color: #b16286">download</strong> the image <span style="color: #3588E9">--></span> <code style="color:#689d6a">docker pull nginx</code>
	- it pulls the image and stores on the host, it doesn't run the container.
- To <strong style="color: #b16286">upload</strong> an image <span style="color: #3588E9">--></span> <code style="color:#689d6a">docker push</code>
	- it sends a docker image to a public or private registry
- To <strong style="color: #b16286">execute a command</strong> on a container <span style="color: #3588E9">--></span> <code style="color:#689d6a">docker exec [container_name]</code>
	- Ex: <code style="color:#689d6a">docker exec silly_sammet cat /etc/hosts</code>
- To <strong style="color: #b16286">attach back</strong> to the running container <span style="color: #3588E9">--></span> <code style="color:#689d6a">docker attach [id]</code>
- To <strong style="color: #b16286">create</strong> an image <span style="color: #3588E9">--></span> <code style="color:#689d6a">docker build -t webapp-color .</code>
	- <code style="color:#689d6a">-t</code> <span style="color: #3588E9">--></span> add a tag
	- <code style="color:#689d6a">.</code> <span style="color: #3588E9">--></span> indicates the current directory


Whenever a new image is created or an existing image is updated, it's pushed to the registry and every time anyone deploys this application, it is pulled from that registry.

Link is a command line option which can be used to link to container together

`docker run -d --name-vote -p 5000:80 --link redis:redis voting-app`
it creates an entrypoiny on ETcd host file one the voting app container, adding and entry with the host name redis whot the internal IP of the redis container.