Available since 2013, Docker is an open platform (engine) written in Go, that allows to develop, deploy, test and run applications as containers. It uses Linux kernel's features to deliver functionality.

Docker isolates applications from infrastructure, including the hardware, operating systems and the container runtime. It uses the namespaces technology to provide an isolated workspace called "container" (containers are isolated from each other).

In container runtime, namespaces can be used to resrct what apps can do by adding or removing Linux capabilitires from it.

capabilities -- linux kernel feature to restrict the set of system calls processes within the namespace can make. 
groups of privileges that can be bestowed onto applications 
allows apps to receive or not admin powers

Docker creates a set of namespaces for every container and each aspect runs in a separate namespace with access limited to that namespace.

>[!info]
><span style="color: #d65d0e">namespaces</span> is a <strong>feature of the Linux kernel</strong> that allows to provide complete network isolation to different processes on the system. It's similar in concept to what a <span style="color: #d65d0e">Hypervisor</span> does to provide the virtual resources to the Virtual Machine.

Namespaces keep containers isolated until docker administrator allows containers to communicate over docker virtual network on the same host. 

The processes running inside the container are in fact processes running on the underlying host. With process ID namespaces, each process can have multiple process IDs associated with it.

By default there is no restriction as to how much of a resource a container can use, and hence a container may end up utilizing all of the resources on the underlying host.

Docker uses <span style="color: #d65d0e">cgroups</span> (control groups) to: 
1. Monitor and restrict CPU usage, or the amount of CPU time each container can take up.
2. Monitor and restrict network and disk bandwidth
3. Monitor and restrict memory consumption (more common)

>[!info]
>The usage of Control Groups makes easier to prevent busier, or larger containers from eating up all the system's resources and slowing other container down without having to carve up significant amount of memory like virtual machine do.

Obs: Control Group can not be used to assign dick quotas to containers.

To limit CPU usage:

```shell
docker run --cpus=.5 ubuntu
```

To limit memory usage:

```shell
docker run --memory=100m ubuntu
```

docker does not shows debug level jobs by default.

enable debug logging:
in docker desktop
`docker run -it --rm --privileged --pid=host guilhermeoliveira` to enter the terminal

sudo sh -c 'echo "{\"debug\": true}" > /etc/docker/daemon.json'
sudo service docker restart

To debug docker in real-time:

```shell
sudo journalctl -f -u docker
```

Docker requires that virtualization to be enabled in the Bios, <span style="color: #d65d0e">VT-X</span> or <span style="color: #d65d0e">AMD-V</span>.

>[!note]
> The main purpose of Docker is to package and containerized applications and to ship them and to run them anywhere any time as many times is needed.

<strong style="color: white">Best practices:</strong>
- use verified images <span style="color: #3588E9">--></span> use a container image scanner if using a verified image isn't possible. Example: Clair, Trivy or Dagba.
- avoid tagging as latest <span style="color: #3588E9">--></span> version tags can be overridden making rollback difficult 
- use non-root users <span style="color: #3588E9">--></span> it makes the containers more secure.

<strong style="color: white">Limitations:</strong>
- Native only runs on Linux
- Container images are bound to their parent operating systems (tied to the Kernel)

The <span style="color:#98971a">portainer</span> is a tool that allows to view and manage in the browser all docker containers. To use it just run it as a docker container, by default it runs on port 9443.

>[!example] Example - portainer
>```shell
>$ docker volume create portainer_data
>
>$ docker run -d -p 8000:8000 -p 9443:9443 --name portainer --restart=always -v /var/run/docker.sock:/var/run/docker.sock -v portainer_data:/data portainer/portainer-ce:lts
>
>$ docker run -d -p 8000:8000 -p 9443:9443 --name portainer --restart=always -v /home/guilherme/.lima/docker/sock/docker.sock   -v portainer_data:/data portainer/portainer-ce:lts
>```
##### <span style="color: #689d6a">Docker Engine</span>

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

Obs: the <span style="color:#98971a">docker daemon</span> can also communicate with other daemons to manage Docker services.

The Docker engine uses namespaces to isolate what's happening in a  running container from the Operating System that hey are running. With namespaces, the Kernel resources, such as process ID, users ID, network, storage, can all be virtualized and share between the host Operating System and the container running on top of it.

>[!note]
>Namespace is similar in concept to what a hypervisor does to provide virtual machine to the VM. They keep containers isolated until docker administrator allows containers to communicate over docker virtual network on the same host. 
##### <span style="color: #689d6a">Docker Architecture</span>

Docker is based on client-server architecture which provides a complete application environment. Docker components includes the client, the host, and the registry.

Docker hosts are also called nodes, and they also include and manage: Images, Containers, Namespaces, Networks, Storage, Plugins and add-ons.

Docker stores and distributes images in a <span style="color:#98971a">Registry</span> (stateless and high scalable application) <span style="color: #3588E9">--></span> the access is public or private, such as <span style="color:#98971a">Docker Hub</span> (default public registry which is cloud-based), Private (implemented for security).

>[!info]
>Registry locations are either hosted on thirds party providers (such as IBM cloud Container registry) or self-hosted in private data center or in the cloud.
>
> registry access: <span style="color:#689d6a">PUSH</span> <span style="color: #3588E9">--></span> [<span style="color:#98971a"> registry </span>] <span style="color: #3588E9"> --> </span> <span style="color:#689d6a">PULL</span>
> <strong style="color: #d65d0e">image:</strong> <code style="color:#689d6a">[Registry]/[User/Account/Image/Repository]</code> <span style="color: #3588E9">--></span> <code style="color:#689d6a">docker.io/library/nginx</code>

The <span style="color: #d65d0e">Docker Registry</span> is itself another application, and it's available as a Docker image.

The two main Docker components, Client and Server (host), communicate via socket, that can be a network socket where the Client is running on one computer and the Server in another computer in a <span style="color: #d65d0e">Cloud Provider</span>, or they can be running on same hardware, with the Server in a virtual machine, which a common case.

<span style="color: #3588E9">--></span> When the Client and the Server are running on the same computer, they connect through a special file called socket. The Client can run even run inside Docker itself.

>[!info]
>Docker also uses "copy-on-write" file systems to build images.

<span style="color:#98971a">copy-on-write</span> <span style="color: #3588E9">--></span> Docker takes each layer, split them and make them into `gzip` files and ships them over the network separately, and the receiving end of that connection (running Docker server) receives all those layers separately and then puts them together using the file system.

<span style="color: #d65d0e">Docker Enterprise</span> provides the Universal Control Plane (UCP) and <span style="color: #d65d0e">Docker Trusted Registry</span> (DTR). Docker EE contains not only the container runtime but also <span style="color: #d65d0e">Docker Swarm</span> orchestration, docker volumes, networking and security.

UCP include centralized policy management for all containers centralized role-based access control, user management, application cluster management and the ability to organize the container as services and stacks.

DTR is an on-site, on-premises registry for centralized storage for all the containers images. It can also include secure image scanning and continuous monitoring of the images in the registry.

Leases are used within Container D to manage how the image used within the Docker daemon.
###### <span style="color:#98971a">Container</span>

A Docker container is a runnable instance of an image, it encapsulates everything an application needs to run. It can be created, stopped, started or deleted using the Docker API or the Docker CLI.

All Docker container are nothing more than a process, looked from the perspective of the operating systems. When it starts the container automatically gets a random ID and a name created for it by Docker.

To <strong style="color: #b16286">add a name</strong> to the container:

```shell
docker run --name=app_container [image_name]
```

```shell
docker run --name app_container [image_name]
```

>[!info]
>In Docker, the container starts with an init process and vanishes when this process exits. To keep a long running container, its necessary to specify what the <span style="color: #d65d0e">Process ID 1</span> is. If that process is gone, the container will stop.

When running a container it's a good strategy to remove the container as soon the application finish executing. This can be done by the `--rm` flag.

```shell
docker run --rm -it --name app_container [image_name]
```

Containers are independent of the storage containers. Depending on the storage layer, in some cases it may run out of layers. Some storage have a limited number of layers.

To <strong style="color: #b16286">copy a file</strong> to a container:

```shell
docker cp local_folder/. container_name:/path_inside_container
```

```shell
docker cp dummy/. brogin_vaughan:/test
```

To <strong style="color: #b16286">copy a file</strong> from a container:

```shell
docker cp brogin_vaughan:/test local_folder
```

To <strong style="color: #b16286">use a non-root user</strong> to run a container:

```shell
docker run --rm -it --user raziel image:v1.0.1
```

docker container have a minimal default set of capabilities. but container's capabilities can be changed with the `docker run` command.

create a container that creates a file and changes its ownership 

`docker run --entrypoint sh --rm alpine -c 'touch .tmp/file && chown 1001:1001 /tmp/file && echi "Fiel permission changed" ' `

disable the capability from the container 

`docker run --entrypoint sh --cap-drop --rm alpine -c 'touch .tmp/file && chown 1001:1001 /tmp/file && echi "Fiel permission changed" ' `

`--cap-drop` --> informs docker to remove a capability from a container

The capability that allows to change file ownership is called `CAP_CHOWN`. 

To add a capability: `--cap-add`

container can be assigned with multiple capabilities

`docker run --entrypoint sh --cap-add CHOWN --cap-add CAP_LEASE --rm alpine -c 'touch .tmp/file && chown 1001:1001 /tmp/file && echi "Fiel permission changed"' `

to inform docker to add or remove all capabilities for a container. `cap-add` takes prececdence over `cap-drop`. use cap-drop all and then add capabilities back with cap-add

`docker run --entrypoint sh --cap-add CHOWN --cap-drop ALL --rm alpine -c 'touch .tmp/file && chown 1001:1001 /tmp/file && echi "Fiel permission changed"' `

to give contaier direct access to specied devices on the system:

`docker run --device` mostly useful if a container needs to use USB devices or GPU cards without granting it a full suite of other privileges.

`--privileged` this flag tell docker to treat a container as if it's a ral process in teh system 

###### <span style="color:#98971a">Image</span>

A Docker image is a read-only template/blueprint with instructions for creating Docker container. Multiple containers can be created based on the same image.

Obs: an image is not the container itself, it only serves a template for the container to run, in other words, the container is based on an image.

Docker caches every instruction result and when the image is rebuilt it will use these cached result --> layer based architecture.

<span style="color:#98971a">Docker images</span> consist on multiple layers (1 instruction = 1 layer), which are <strong>Read-Only</strong>, and each of these layers has an unique ID. The layer optimize build speed (caching) and re-usability. 

Each <span style="color: #d65d0e">layer</span> is only a set of differences from the layer before it, the layers are stacked on top of each other. When an image is run as a container a new <span style="color: #d65d0e">writable layer</span> (container layer) is added, which allows to make changes to the container. The last layer is an image usually, but not always, contains instructions for configuring the container.

>[!info]
>Multiple containers are typically based on the same image, called <span style="color: #d65d0e">base image</span>. Changes made to the base image are actually stored in a new layer and don't the base layer.

All changes made to the running container, are written to the container layer. But the files won't be persistent after the container is deleted. To write data in the writable layer of the container, Docker uses <span style="color: #d65d0e">storage drivers</span>.

Docker uses storage drivers to enable layered architecture. Some of the common storage drivers are: AUFS, ZFS, BTRFS, Device Mapper, Overlay, Overlay2. The selection of the storage driver depends on the underlying OS.

storage drivers define how layers are stored on disk and represented to containers. In other words, storage drivers are responsible for decompressing layers into a directory structure, and presenting them to a container as a fake route directory. 

Some container run times refer to storage drivers as graph drivers or snapchatters.

overlway2 is the most popular storage driver. 

>[!info]
>Docker will choose the best storage driver available automatically based on the operating system.

<span style="color: #d65d0e">Layers</span> are saved on disk only once and can be shared between images, which saves disk space and network bandwidth.

Every image has its own internal file system which is totally detached from the file system on the machine that docker is running. It's hidden away inside the Docker container. 

Each image will contain a manifest at the root levels that provide more information about itself, including the relationship between its layers. The container runtime uses manifests as guides for layers that should be extracted and their containers configured.

To <strong style="color: #b16286">inspect</strong> an image:

```shell
docker image inspect [image_id]
```

To view each layer of an image the <span style="color:#98971a">dive</span> tool is a good choice. It extracts the image from the Docker Engine and it show in the terminal a detailed information about each layer of container image. 

```shell
dive [image_name]
```

<span style="color: #d65d0e">Tags</span> are essentially <strong>aliases</strong>, an image can have multiple tags, but all points to the same source image. The tag <code style="color:#689d6a">latest</code> is a tag associated to the latest version of a software, which is governed by the authors of that software.

>[!note]
> Each version of the software can have multiple short and long tags associated with it

To <strong style="color: #b16286">tag</strong> an image:

```shell
docker image tag [source_image]:[tag] target_image:[tag]
```

```shell
docker image tag my-webapp:v1 my-webapp:nginx
```

<span style="color: #d65d0e">Dangling images</span> are images that are not tagged and are not referenced by any container.

To <strong style="color: #b16286">remove</strong> dangling images:

```shell
docker image prune
```

A <span style="color: #d65d0e">Docker repository</span> within a registry is a collection of related Docker images with the same name but different tags. Each image is stored as a tag that can refer to different variations of an image.

>[!note]
>many companies choose to run their own registry within their own company to ensure that their data stays safe and private

Naming a Docker image: 
- <code style="color:#689d6a">[registry]/[repository]:[tag]</code> <span style="color: #3588E9">--></span> <code style="color:#689d6a">docker.io/ubuntu:18.04</code>

To pull (download) an image:

```shell
docker pull [image_name]
```

To push an image:

```shell
docker push [image_name]
```

To search for images in Docker Hub:

```shell
docker search python
```

The `--filter` option allows to filter search results:

```shell
docker search --filter is-official=true python
```

To log into Docker Hub:

```shell
docker login
```

>[!info]
>Docker saves the credentials for Docker Hub in the home directory, so that it can easily login in the feature.

To push the image into a registry:

```shell
docker image tag my-server username/my-server:0.0.1
```

```shell
docker push username/my-server:0.0.1
```

To pull the image from registry:

```shell
docker pull username/my-server:0.0.1
```

The image can also be pulled using the IP address

```shell
docker pull 192.168.56.100:5000/my-server
```

To run the container from the private registry:

```shell
docker run -d -p 5000:5000 --name registry registry:2
```
###### <span style="color:#98971a">Network</span>

Docker provides the ability to access network port within the container with port binding --> feature that allows to take a port of the host machine and map to a port within the container. 

To map ports for the container:

```shell
docker run -d --name my-server -p 5001:5000 my-server
```



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

multiple containers can be added into the same network, by using the `--network` option. on the `docker run` command. 

Within a Docker network, all containers can communicate with each other and IPs are automatically resolved.

`docker network create ` --> create a docker internal network
`docker network create favorites-net`
`docker run -d --name mongodb --network favorites-net mongo`
`docker run --name favorites --network favorites-net -f --rm -p 3000:3000 favorites-node`

to allow communication between the applications running in a container to the host achine machine just use the address `host.docker.internal`

Docker Networks actually support different kinds of "**Drivers**" which influence the behavior of the Network. The default driver is the "**bridge**" driver
The driver can be set when a Network is created, simply by adding the `--driver` option. `docker network create --driver bridge my-net`

Docker also supports these alternative drivers - though you will use the "bridge" driver in most cases:

- **host**: For standalone containers, isolation between container and host system is removed (i.e. they share localhost as a network)
    
- **overlay**: Multiple Docker daemons (i.e. Docker running on different machines) are able to connect with each other. Only works in "Swarm" mode which is a dated / almost deprecated way of connecting multiple containers
    
- **macvlan**: You can set a custom MAC address to a container - this address can then be used for communication with that container
    
- **none**: All networking is disabled.
    
- **Third-party plugins**: You can install third-party plugins which then may add all kinds of behaviors and functionalities
###### <span style="color:#98971a">Storage</span>

A volume is a directory on the host machine that is accessible to a container. When a Docker volume is used, the data inside it is not stored in the container's file system, but in the host machine's file system --> the data in a volume persists even if the container is deleted or recreated.

A volume and be created using the `docker volume create` command.

>[!example] Example - docker volume
>```shell
>docker volume create d_volume
>```
>Obs: creates a folder called d_volume under the `/var/lib/docker/volumes` directory.

To list all available volumes:

```shell
docker volumes ls
```

To inspect a volume:

```shell
docker volumes inspect [volume_name]
```

To attach a volume to a container, use the `-v` or `--volume` option:

```shell
docker run --rm -v [/host_path]:[/container_path]
```

Volumes are a good option for persisting data across different container. Volumes can be used to store data from a database outside the container.

While volume and bind mount can be used to share data between the host machine and a container, they work differently and have different use cases.

Unlike Docker volume, the data inside a bind mount is not stored outside the container. If the container is removed, the data will be lost.

volume mounting --> feature allows Docker to map a folder from the host machine to a folder in the container. This can be done by using the `--volume` or `-v` option.

>[!example] Example - volume mounting
>Example 1
>```shell
>docker run --rm --entrypoint sh -v /tmp/container:/tmp ubuntu -c "echo 'Hello World.' > /tmp/file && cat /tmp/file"
>```
>Example 2
>```shell
>docker run --name website -v $PWD/Documents/website:/usr/share/nginx/html -p 8080:80 --rm nginx
>```

Docker uses volumes and bind mounts to persist data even after a container stops
built int feature, 
it helps with persistent data 

values are folders on the host machine hard drive with are mounted ("mapped") into containers. values persist if a container shuts down. If a container (re)-stars and mounts a volume, anu data inside of the volume is available in the container. 
A container can write data into a volume and read data from it.

A defined path in the container is mapped to the create volume / mount.

volumes --> managed by docker
- anonymous volumes  --> created specifically for a single container, attach to a container, can be used to save (temporary) data inside the container
- named volumes --> volumes persist even if the container is shut down, as the folders in the hard drive. good for data which should be persistent but which it doesn't need to be edit directly. 

anonymous volumes are **removed automatically**, when a container is removed
with the `--rm` option container are remove automatically when a container is removed. If you start a container **without that option**, the anonymous volume would **NOT be removed ** even if you remove the container (with `docker rm ...`).

docker sets ups a folder / path on the host machine, the exact location in unknown to the user. and it's managed by the `docker volumes` command. 

Docker stores all its data by default on this location: `/var/lib/docker`

To persist data, it's necessary to mount a volume or map a directory outside the container on the docker host or host to a directory inside the container.

`docker run -v /app/data/ ...` --> creates an anonymous volume
`docker run -v data:/app/data ...` --> creates a named volume
`docker rum -v /path/to/code:/app/code ...` --> creates a bind mount

`docker volume rm VOL_NAME` or `docker volume prune` to remove **unused anonymous volumes**

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
- <span style="color:#98971a">bind mounting</span> <span style="color: #3588E9">--></span> mounts a directory from any location on the Docker host (host machine) . good for persistent, editable data.

>[!example] bind mount
>```shell
>docker run -v /data/mysql:var/lib/mysql mysql
>```

>[!example] --mount option
>```shell
>docker run -it -d -p 5000:5000 --mount type=bind,source="${PWD}/test",target=/app/test big-star-collection:v2
>```
>The source is the location on the host and the target is the location on the container.

mounts are useful when you need to share code or configurations files between the host machine and the container during development or testing.

with the `--mount` flag if a directory specified does not exist on the host, it will return an error, but `-v` flag will create it.

We use this bind Mount during development to reflect changes in our code, into running container instantly. Because if the container is running in production on a server, there is no connected source code, which updates while it's running.

bind mount:
`docker run -d -p 3000:80 --rm --name feedback-app -v feedback:app/feedback -v "home/user/guilherme/dev:/app" -v feddback-note:volumes`

`-v $(pwd):/app`

by default volumes are read write, --> the container is able to read data from there and write data to them.

to ensures that docker will now not be able to write into this folder or any of its sub-folders.

`docker run -d -p 3000:80 --rm --name feedback-app -v feedback:app/feedback -v "home/user/guilherme/dev:/app:ro" -v feddback-note:volumes`

How can I get my web server to access the database on the database container?

The right way to do it is to use the container name. All containers in a docker host can resolve each other with the name of the container. Docker has a built in DNS server that helps the containers to resolve each other using the container name.

How were the containers isolated within the host?
Docker uses network namespaces that creates a separate namespace for each container. It then uses virtual Ethernet pairs to connect containers together.

Obs: Bind mount shouldn't be used in Production!

to remove all volumes with prune:
`docker system prune --volumes -f`
###### <span style="color:#98971a">Multi-app images</span>

use an entrypoint script that execute other program in the background, then run with `docker run --init` --> configurdd the container to run th entrypont script whithin a process supervisor called tini --> watchs every process runnign in the container and makes sure that signal are passed coreeclty to them.

install and configure systemd in the image

use amore sophiscated process supervisor, like s6-overlay --> it does the same job as Tini, but it also allows users to express multiple service in convenient directory structure. 

docker run -e APP_USER=Guilherme --rm test=app
###### <span style="color:#98971a">Registry</span>

The image registry is a web server that serves container images. The difference between a regular web server from an image registry is how the images are laid out.  

Registries use a particular folder structure to make it easy fro docker to find images and verify that hey are who they claim to be.

The Image Registry works seamlessly with Docker pull.

Ways to create a registry:
- run the registry as a container from Docker's official image
- front the registry with a reverse proxy

Using the Docker's official image:

create the container that will run the registry

```shell
docker run --rm --name registry -p 5000:5000 -d registry:2
```

push the image into the registry

docker tag my-image:latest localhost:5000/my-image:latest
localhost:5000 --> DNS Label of the registry
docker push localhost:5000/my-image:latest --> tells Docker to upload the image into the registry

create the manifest list:

docker manifest create --insecure localhost:500 /my-image --amend localhost:5000/my-image:latest

image digest is created by the registry when images are pushed up to it.
the `manifest create` command will query the registry for the digest for the images added to the list with the `--amend` flag.

confirm if the digest matches the image:

```shell
docker images --digests localhost:5000/my-image
```

push the manifest list up into the registry:

```shell
docker manifest push localhost:5000/my-image
```

delete all images

```shell
docker images | grep my-image | awk '{print $3}' | xargs docker rmi -f 
```

`awk '{print $3}'` --> display the third column
`xargs` --> it takes each line and feed it to the next command

multi-platform images are manifest list to contain different image digests for different processor platforms --> allows to create an image that works on ARM processors as well as X86 processors.

simple registries are limited:
they are insecure
the only speak HTTP
they are not very configurable

a reverse proxy in front of the registry solves those issues
reverse proxy is a web server that internally intercepts and forwards traffic it receives, to a destination that's usually an internal device. 
a reverse proxy will usually forward the request to some other address. 

using nginx:
create a docker network for the registry
create a self-signed certificate and private key
create an authentication files to use credentials
recreate the registry
create an nginx web server as a reverse proxy in front of the registry

Obs: manifest list do not work with local secure registries.

`docker network create registry`

`./create_unsigned_certs.sh` --> run a program called Open SSL within the container a container that will generate the self-signed certs. 

add the `cert.pem` into the virtual machines list of root certificate authorities
`sudo cp ./certs/cert.pem /usr/local/shre/ca-certificates/registry.crt`
`sduo update-ca-cerficiates` --> script that update the root certificates

configure the web server with the credentials
`docker run --entrypoint htpasswd httpd:2 -Bbn admin supersecret > ./htpasswd`
`htpasswd` --> tool that creates file that configure basic authentication on web servers.

`docker run --rm --name registry-backend --network registry -d registry:2`

`docker run --rm -v $PWD/nginx.conf:/etc/nginx/nginx.conf -v $PWD/htpasswd:/auth/htpasswd -v $PWD/certs:/certs --network registry -p 5000:5000 -d nginx`

log into the local registry:
`docker login localhost:5000`

certificate root authorities are special certificates used by just about every app that talks HTTPS, for verifying client and service certificates.
##### <span style="color: #689d6a">Docker CLI</span>

The `--help` flag works with every Docker command, which shows information about a command and how to use it.

```shell
docker network --help
```

To <strong style="color: #b16286">create</strong> a docker container:

```shell
docker container create hello-world:linux
```

>[!note]
>If the image doesn't exist in the machine, Docker will try to retrieve it from a container image registry. By default, Docker always tries to pull from Docker Hub.

To <strong style="color: #b16286">list</strong> running containers:

```shell
docker container ls
```

```shell
docker ps # old syntax
```

To <strong style="color: #b16286">list</strong> all containers:

```shell
docker container ls -a
```

```shell
docker ps --all # old syntax
```

To <strong style="color: #b16286">start</strong> a container:

```shell
docker start container_id
```

To <strong style="color: #b16286">see the logs</strong> of a container:

```shell
docker logs container_id # can be the image's name as well
```

<strong>Obs:</strong> The <code>-f</code> flag can be used to keep listening the container.

An option to the `logs` command is to start the container and "attach" the terminal to the container's output:

```shell
docker container start --attach container_id
```

The short way to <strong style="color: #b16286">run/start</strong> a container:

```shell
docker run hello_world:linux
```

Obs: `Docker run` attaches to the container after it start it.

The <code style="color:#689d6a">-d</code> option for detach mode, runs the in the background mode.:

```shell
docker run -d my-server
```

To  <strong style="color: #b16286">execute a command</strong> on a container:

```shell
docker exec d90d date
```

The `exec` command can be used to start terminal sessions within the container. To enter keystroke the command must be interactive.

```shell
docker exec --interactive --tty d90d bash
```

Short way to enter commands:

```shell
docker exec -i -t d90d bash # or -it
```

To <strong style="color: #b16286">get a snapshot </strong>of the container's performance:

```shell
docker stats [container_name]
```

To <strong style="color: #b16286">show information</strong> about a container:

```shell
docker inspect [container_name] # shows info in JSON format
```

To <strong style="color: #b16286">debug</strong> a slow container:

```shell
docker top [container_name]
```

To <strong style="color: #b16286">stop</strong> a container:

```shell
docker stop fd69 # can be the container name as well
```

```shell
docker kill container_name
```

The `kill` command sends the kill signal which can not be blocked or handled. The killed child process doesn't notify its parent that it received the kill signal, which can cause errors.

To <strong style="color: #b16286">force the stop</strong> of a container: 

```shell
docker stop -t 0 79f6 # can lead to data loss
```

To <strong style="color: #b16286">remove</strong> a container permanently:

```shell
docker container rm [container_id]
```

```shell
docker rm [container_id] # old syntax
```

The `rm` command doesn't stop containers that are running, to do this use the `-f` option to remove running containers.

```shell
docker container rm -f [container_id]
```

To <strong style="color: #b16286">list all</strong> available images:

```shell
docker image ls
```

To <strong style="color: #b16286">remove</strong> an image:

```shell
docker image rm [container_name]
```

```shell
docker rmi [image_id] # old syntax
```

When removing an image if the `-f` flag is used, it will force the image to be removed even if it's attached to a running container.

To <strong style="color: #b16286">remove</strong> useless data:

```shell
docker system prune
```

The `system prune` command, prunes all unused images, containers and networks.

To <strong style="color: #b16286">modify</strong> the entry point during runtime: 

```shell
docker run --entrypoint sleep2.0 ubuntu-sleeper 10
```
##### <span style="color: #689d6a">Dockerfile</span>

The Dockerfile is a language for creating and describing docker container images. Dockerfile is the name of the language, as well as the default name of the file that Docker looks for when creating container images. 

Every Dockerfile consist of a set of commands (instructions), each on their own line. The instruction is the first word of the statement, every other word after the instruction is provided to is as arguments.

>[!example] Example - Dockerfile
>```dockerfile
>FROM ubuntu
>
>RUN apt-get update 
>
># Define working directory
>WORKDIR /root
>
># Define default command
>CMD ["bash"]
>```
>Docker process Docker file from top to bottom. Each docker instruction on a Dockerfile creates a new layer in the image which is simply built up from multiple layers based on these instructions.

 >[!info]
 >Docker runs each Dockerfile command in an "intermediate container" (temporary container) and saves the results as in an image layer. These layers are joined together to form the image as the Dockerfile is processed.

The byproduct of the command that ran in the container is saved into a layer. This layer is added to the the new image, which is given to the intermediate container crated by the next command of the Dockerfile. This process repeats until every command in the Dockerfile is processed.

<strong>Obs:</strong> Command like `LABEL`, `EXPOSE` and `ENTRYPOINT` do not run in intermediate containers.

To build the image from a Dockerfile:

```dockerfile
docker build .
```

In case in the current directory there are more than one Dockerfile, it can be specified using the `--file` or `-f` option.

```dockerfile
docker build -f server.Dockerfile .
```

The `--force-rm` option allows to remove any intermediate containers that exist, even if the build is unsuccessful.

```dockerfile
docker build --force-rm=true .
```

The `--rm=true` option can also be used in case of unsuccessful build. The intermediate container will not be removed. This allows for debugging the last intermediate container or committing it as an intermediate image.

```dockerfile
docker build --rm=true .
```

>[!note]
>The context is simply the folder containing files that Docker will include in the image.

The `--no-cache` option cane be used to skip the cache and rebuilt the entire image. It's useful in case the installation depends on external resources.

```dockerfile
docker build --no-cache .
```

If the Dockerfile is elsewhere the path to it must be informed:

```dockerfile
docker build ~/Dockerfiles/ubuntu/
```

When Docker finishes running the Dockerfile, the resulting image will be on the <span style="color: #d65d0e">local registry</span>.

Each step of running a Dockerfile is cached, Docker skips lines that haven't changed since the last build. dot here, we tell Docker that the Dockerfile will be in the same folder as we're running this command in.

If the name of the source image is defined without a tag, the default tag will be used, which is latest. When there's no tag defined, Docker assumes that the image that's being created is the latest version of the images in the repository.

To build an image with a tag:

```dockerfile
docker build -t my-webapp:v1 .
```

When creating a new version of an image, the `build` command must be used to rebuild the image with a new image ID --> good for keeping each version separate.

```dockerfile
docker build --no-cache -t my-webapp:v2 .
```

To run a container based on a Dockerfile:

```dockerfile
docker run container_id -p 3000:80
```
###### <span style="color:#98971a">Dockerfile Commands</span>

<code style="color: #689d6a">FROM</code> <span style="color: #3588E9">--></span> defines the "base" image that the Dockerfile's image will be created from. It links the current image to the new image.

>[!example] Ways to use FROM command
>Select the "latest" tag of an image
>```dockerfile
>FROM ubuntu
>```
>Select the tag of an image
>```dockerfile
>FROM ubuntu:kinetic
>```
>Select the "latest" tag of an image and git it an alais (multi-stage build only)
>```dockerfile
>FROM ubuntu AS base
>```
>select the tag of an image and git it an alias name (multi-stage build only)
>```dockerfile
># FROM $image:$tag AS $name
FROM ubuntu:kinetic AS base
>```

<code style="color: #689d6a">COPY</code> <span style="color: #3588E9">--></span> adds files and directories into Docker images from a provided context

>[!example] Ways to use COPY command
>Copy files into files
>```dockerfile
>COPY ./my-file.txt /app/my-file.txt
>```
>Copy files into drectories
>```dockerfile
>COPY ./my-file.txt /app/
>```
>Copy directories into directories
>```dockerfile
>COPY ./my-dir /app/
>```
>The first argument is the file or directory within the context to be copied. The second argument is the path inside of the container that file or directory in the first argument will be copied into

Using **wildcards** on arguments:

The `?` to replace single characters in a file or directory

```dockerfile
COPY song/ song-?.mp3 /songs
```

The `*` to copy files or directories that start with a specific word

```dockerfile
COPY songs/ song* /songs
```

Two useful <code style="color: #689d6a">COPY</code> arguments:

`--chown` <span style="color: #3588E9">--></span> to set a user in group on a directory or file copied into Linux-based container images. Useful if the app running within the container image will run as a different user that the user created in its based image.

`--link` <span style="color: #3588E9">--></span> to copies files or directory from context into a blank layer.

<code style="color: #689d6a">ADD</code> <span style="color: #3588E9">--></span> old version of <code style="color: #689d6a">COPY</code>, also works with URLs to TAR files

>[!note]
>Obs: use COPY instead of ADD wherever possible.

When adding or coping a file to the Docker container it's a good practice to use a sub folder instead of entering the root folder.

>[!example] Example  
>```dockerfile
>COPY . /app
>```
>All the files from the machine will be copied into the `.app` folder inside the container. If it doesn't exist the folder will be created in the image. 

COPY . ./ <span style="color: #3588E9">--></span> current working directory inside of our Docker container.

to restrict what is copied to the container, add a `.dockerignore` file to the project.
specify which folders and files, should not be copied by a copy instruction. just as using `.gitignore`

container created by docker run are non interactive by default --> contaienrs are not configured to not accept input like keystrokes. 

<code style="color: #689d6a">RUN</code> <span style="color: #3588E9">--></span> executes commands within temporary containers. 

>[!example] Ways to use RUN command
>Shell form
>```dockerfile
>RUN echo "Hello, word!"
>```
>Exec form
>```dockerfile
>RUN ["echo", "hello, world!"]
>```
>Commands in shell form runs inside os a shell, but the sub-process created will be forked from a shell.
>
>Commands written in exec from are run directly within the container without a shell --> any input sent to the container will go directly to the app.

<code style="color: #689d6a">ENTRYPOINT</code> <span style="color: #3588E9">--></span> configures the container image to run an application when a container is created from it. It takes two forms, just like the RUN command. But the form affects how the application behaves. 

Shell Form:
- App runs as a child of /bin/sh or cmd
- Any signal sent to the app are caught by the shell, not the program
- Any code in the app that relies on signals will not run
- Arguments sento to containers will get passed into the shell, not the program
- Environment variables, pipes, or any shell feature can be leveraged, but an entrypoint script is much more reliable.

>[!note]
>In case of a started containerized app from an image in Docker Hub and it won't forcefully stop with control Z, it most likely because of entrypoint.

The `entrypoint` script pattern simply takes all of the logic in a Dockerfile in shell form and put it into its own script that is invoked with exec form.

>[!example] ENTRYPOINT command:
>```dockerfile
>RUN apt -y update && apt - install curl
>ENTRYPOINT [ "/app/app.sh" ]
>
># /app/entrypoint.sh
>#! /usr/bin/env bash
>SOME_VAR=$SOME_VALUE_FROM_DOCKER;
>[ "$SOME_VAR" == "foo" ] && /app/app.sh --foo || /app/app.sh --bar
>```
>entrypoint scripts makes the Dockerfile easier to read and debug without removing control from the app like the shell form does.

Exec form: 
- App runs as the top-level process within the container (as PID 1)
- Any signal sent to the app are sent to the program
- Arguments sent to the container will get passed in the program

<code style="color: #689d6a">CMD</code> <span style="color: #3588E9">--></span> stands for command. Sim,ilvar o entrypoint, it configures tcontainer to run an application on startup. It dependes wheter an Entryint is provided or not, and wheter CMD is writtent in sheel or exec form. is best suited from providingf default argument to an Etntrypoint.

The are four types of combinations with CMD and ENTRYPOINT:
- ENTRYPOINT missing, CMD provided  <span style="color: #3588E9">--></span> `/app/app.sh` is run as PID 1. Arguments provided to it are sent to `/app/app.sh`.
- ENTRYPOINT provided, CMD provided
- ENTRYPOINT provided, CMD missing  <span style="color: #3588E9">--></span> `/app/app.sh` is run as PID 1. Additional arguments provided to it are sent to `/app/app.sh`.
- ENTRYPOINT missing, CMD missing  <span style="color: #3588E9">--></span> CMD or ENTRYPOINT is inherited from base image, or `/bin/sh -c` or `cmd /S /C` is used as default ENTRYPOINT.

>[!example] CMD command:
>Option 2
>```dockerfile
>FROM ubuntu
>COPY ./app
>RUN apt -y update && apt -y install curl
>ENTRYPOINT [ "/app/app.sh" ]
>CMD [ "--argument" ]
>```
>`--argument` is provided as an argument to `/app/app.sh`. Additional arguments provided to it, are sent to `/app/app.sh`
>
>Option 3
>```dockerfile
>ENTRYPOINT [ "/app/app.sh" , "--argument" ]
>```
>The argument is part of the app, so it can't be override it. Any argument typed with `docker run` will be appended into the program.

ARG --> defines build arguments, which are variables provided at build time.

>[!example] ARG command:
>```dockerfile
>FROM ubuntu
>ARG curl_bin=curl
>COPY . /app
>RUN apt -y update && apt -y install "$curl_bin"
>CMD [ "--argument" ]
>ENTRYPOINT [ "/app/app.sh" ]
>```
>Obs: The `--build-arg` flag must be used during 'docker build' to set variables defined with the ARG command.
>```shell
>docker build \ 
>  --build-arg curl_bin="curl=7.81.0" \
>  -t my-image \
>  .
>```

>[!note]
>If the `--build-arg` is not used the image might not behave the way it was expected to, event if the build was successful.

ENV --> defines environment variables that containers started from an image should receive. 

>[!example] ENV command:
>```dockerfile
>FROM ubuntu
>ENV curl_bin="curl=7.85.0"
>COPY . /app
>RUN apt -y update && apt -y install "$curl_bin"
>CMD [ "--argument" ]
>ENTRYPOINT [ "/app/app.sh" ]
>```

>[!info]
>ENV variables are great for providing default configuration for apps while still allowing users to change them when they start containers with 'docker run'

Differences between  ENV and ARG
- ENV variables are defined for every container started from an image; ARG variables are only used during runtime.
- ARGs are set at build time, ENVs are set at run time --> it can't be override through docker build, environment variables can only be override is by using the `-e` or `--env` flag with docker run. 

Similarities between  ENV and ARG
- Both ENV and ARG can only be expanded within Run commands
- ENVs and ARGs used by RUN commands must precede the RUN commands that reference them

LABEL --> allows to document the images by adding metadata to them. Accepts a key-value pair. The most popular LABEL in Docker image is the maintainer.

>[!example] LABEL command:
>Option 1
>```dockerfile
>LABEL maintainer="Guilherme Oliveira <dev@guilhermeoliveira.me>"
>LABEL version="1.0"
>LABEL description="This is a webapp built with flask"
>```
>Option 2
>```dockerfile
>LABEL "com.example.vendor"="Big Star Collections" \
>version="1.0" \
>description="The Big Star Collections Website \
>using the Python base image."
>```

WORKDIR --> sets a working directory from RUN commands within the Dockerfile and/or container create from the image. The last WORKDIR will be used by containers.

```dockerfile
WORKDIR /app
```

USER --> sets the Linux or Windows user to be used for RUN command and/or container. 
- Linux users can be numerical.
- It can be used multiple times to change the working directory while building. 
- The last USER command will be used by containers. 
- It prevents container for running as root by default
- The default user can be overridden with `docker run --user`
- Can create users within the Dockerfile for containers to run as later

>[!example] USER command:
>```dockerfile
>USER newuser
>ENTRYPOINT ["/app/app.sh"]
>```
>---
>```shell
>docker run --rm --entrypoint whoami my-image newuser
>```

EXPOSE --> documents network ports that containers created from the image should expose at runtime. It only accepts as arguments the port number.
- By default it assumes TCP ports
- Does not automatically expose ports
- Useful for documentation; completely optional

```dockerfile
EXPOSE 8080
```

VOLUME --> maps a folder in the container to persist data

```dockerfile
FROM node

WORKDIR /app

COPY package.json /app

RUN npm install

COPY . .

ARG DEFAULT_PORT=80

ENV PORT $DEFAULT_PORT

EXPOSE $PORT

CMD ["node", "server.js"]
```

Docker supports build-time arguments and runtime environment variables.
Arguments allow you to set flexible bits of data, in your Dockerfile which you can use in there to pluck different values into certain Dockerfile instructions.
set on image build (docker build) via `--build-arg`

Environment variables on the other hand are available inside of a Dockerfile like arg,
but args are available in your entire application code in your running application.
and you can set them with the `--env` option inside of a Dockerfile,

`docker run -d --rm -p 3000:8000 --env PORT=8000 --name feedback-app`
`docker run -d --rm -p 3000:8000 -e PORT=8000 --name feedback-app`

you can also specify a file that contains your environment variable

```env
PORT=8000
```

`docker run -d --rm -p 3000:8000 --env-file ./.env --name feedback-app`

And args and environment variables allow you to create more flexible images and containers because you don't have to hard-code everything into these containers and images. Instead, you can set it dynamically when you build an image or even only when you run a container.

to build for another environment with a different port value

`docker build -t feedback-node:dev --build-arg DEFAULT_PORT=8000 .`
###### <span style="color:#98971a">Multi-Stage builds</span>

Multi-stage builds use intermediate images to produces smaller final images in a single Dockerfile.

Multi-stage builds can use multiple base images --> produces significantly smaller final images and accelerate build time through improved caching. 

Each group of commands under a base image is called a stage. While each stage in a multi-stage build produces a temporary image, the last stage is the stage used officially create the final image. 

Stages are a zero index <span style="color: #3588E9">--></span> they are count from 0 instead of 1

Multi-stage builds allows to copy files, or directories, between stages. This enable to create images that only have everything that the app needs to run. It's done with the copy command with a `--from` flag.

Stages can be named, which makes referencing them in later COPY operations easier.

>[!example] Example - multi stage build
>Stage 0
>```dockerfile
>FROM ubuntu as base
>ENV curl_bin="curl"
>RUN apt -y update && apt -y install "$curl bin"
>RUN curl -i -sS google.com | \
>  grep -E '^Date:' | \
>  sed 's/^DateL //' | tr -d $'\r' > '/tmp/date.txt'
>```
>Stage 1 (The Final Image)
>```dockerfile
>FROM bash:alpine3.16 AS app
>COPY . /app
>COPY  --from=base /tmp/date.txt /app/include/date.txt
>ENTRYPOINT [ "/app/app.sh" ]
>CMD [ "--argument" ]
>```

Multi-stage builds can copy files or directories from images that aren't in the Dockerfile.

```dockerfile
COPY --from=some-other-image /header.txt /app/include/header.txt
```

Stages can also be used as many times as is necessary. Each stage descends from the image that was created by the stage that's referenced by FROM.

<strong style="color: white">Advantages:</strong>
- Produces significantly smaller final images
- Can be much faster than builder pattern while being less fragile
- Can produce extremely secure images by discarding unnecessary dependencies. 
##### <span style="color: #689d6a">Docker Compose</span>

Docker compose is a tool for defining and running multi-container Docker applications. It allows to define an entire stack, including services, networks, and volumes with a single configuration file and then a set of orchestration commands to start all those services.

Docker Compose can document a system as a runnable configuration file --> compose manifest. It does not add any functionality do the docker ecosystem, but it does make the existing functionality significantly easier to use. Docker Compose works together with Dockerfiles.

>[!example] Example - compose manifest
>```yaml
>services:
>  bookstack:
>    image: lscr.io/linuxserver/bookstack:version-
>    container_name: bookstack
>    # environment:
>      # - DB_USERNAME=bookstack
>      # - DB_PASSWORD=
>    env_file: 
>      - ./env/mongo.env
>    volumes:
>      - ./app_data:/config
>    networks:
>      - bookstack
>    ports: 
>     - 6875:80
>
>networks:
>  bookstack:
>    name: bookstack 
>```

Compose is a declarative tool, and it's self-document. It was designed as a tool for a single hosted server. It's well suited for local  development, staging server, continuous integration testing environment, and it's great for managing multiple containers on the same host.

Obs: It's not designed for distributed system and has no tooling for containers across multiple hosts. Compose was designed for non-production environments only. 

>[!note]
>Every docker compose configuration must be in a yaml file, and be saved under the file name "docker-compose.yaml"

Normal Workflow:
- Dockerfile ---> Docker Build Command ---> Docker Image
###### <span style="color:#98971a">Compose Commands</span>

To build the services:

```shell
docker compose up
```

The `-d` flag allows to run the service in background

```shell
docker compose up -d
```

The `--build` option force docker compose to reevaluate the Dockerfiles and rebuild images if required. It forces docker compose to go through the Dockerfiles again and then recreate the images if something changed.

```shell
docker compsoe up -d --build bookstack
```

To start up only one service:

```shell
docker compose up -d bookstack 
```

To stop and delete all running containers:

```shell
docker compose down
```

The `--volumes` will automatically delete any named volumes:

```shell
docker compose down --volumes
```

To free up memory:

```shell
docker compose stop
```

To start and restart all running containers:

```shell
docker compose restart
```

To validade the docker compose file:

```shell
docker compose config
```

Obs: Thy syntax for using docker compose if it's installed as a part of docker engine is `docker compose`, but in case it's installed as a standalone binary, it must the following syntax: `docker-compose`.

docker compose push --> push the images to docker hub
docker compose logs --> to view the logs of a service 
docker compose logs --tail=10 --> limit the container logs output
docker compose logs --follow --> follow the container log output
docker compose exec service_name shell --> shell into the container 
/bin/bash
###### <span style="color:#98971a">Compose Components</span>

services --> defines the various containers (services) that make up the application. Each service has a name, and under each service, parameters can be configured such as Docker image to use, environment variables, port to expose, volume to mount, etc.

>[!example] Example - service
>```yaml
>services:
>  bookstack:
>    ...
>  bookstack_db:
>    ...

Obs: Docker Compose ser vices can be named anything. They are intended to be human readable and ideally should be meaningful. 

image --> defines the value to be used for the service, it also overrides the image name specified in the Dockerfile.

>[!example] Example - service
>```yaml
>services:
>  bookstack_db:
>    image: mariadb:lts
>```
>Docker Compose will tech the MariaDB image automatically from Docker Hub.

command: This key lets override the default command for the environment. This is useful when you need o specify how the container should start.

```yaml
command: npm start
```

build/context: It defines either a path do a directory containing a Dockerfile, or a URL to a git repository.

>[!example] 
>```yaml
>build:
>  context: ./dir
>```
>---
>```yaml
>services:
>  webapp:
>    build: https://github.com/mycompany/webapp.git
>```

dockerfile --> specifies an altervative Dockerfile for the build

>[!example] 
>```yaml
>build:
>  context: .
>  dockerfile: Dockerfile.dev
>```

Environment variables at docker are visible from inside the running container. The most common and simple use case a Docker environmenr vairnale if for specifying thing like a curret runtime configuration such as dev or prod.

Build arguments are a type ofr environment variable that are available to dockder ony at build ime, bit not inside the contianer. They are useful for specifying a version for a certain build tool or cloud platform configuration.

>[!example] Example - build argument
>```yaml
>services:
>  storefront:
>    build: 
>      context: .
>      args: # can have any name or any value
>        - region=us-east-1
>    environment:
>      - runtime_env=dev
>```
>args --> attribute to pass build arguments to the build context. Useful for dynamically setting values during the build. 
>
>environment --> to set environment variables for the service. Useful for configuring the applications dynamically

Running `export runtime_env=dev` on the host machine and leaving the value out from the Docker Compose configuration will have the same effect as specifying inside the file. 

Obs: use environment files if the lost of variable gets too long.

Compose also supports passing in file paths to an environment configuration.

>[!Example] Example - file paths
>```config
>MYSQL_ROOT_PASSWORD=]p0.3617SR
>MYSQL_DATABASE=bookstack_app
>MYSQL_USER=book_app
>MYSQL_PASSWORD=]p0.3617S
>```
>---
>```yaml
>services:
>  database:
>    image: "mysql"
>    env_file:
>      - ./mysql/env_vars
>```

volumes --> This section allows to define named volumes or bind mounts for the services. Volumes are used to persist data between container restarts.

>[!Example] Example - volumes
>---
>```yaml
>services:
>  bookstack_db:
>    volumes:
>      - ./db_data:/var/lib/mysql:ro
>      - ./db_config:/etc/mysql/conf.d
>```
>./db_data --> source
>/var/lib/mysql --> target

Compose conforms to Bash standads for specifying a direcry path. 
- `./` --> current directory
- `../` --> parent direcotry, one level above the compose fongiuration file
- `/` --> absolut path on the host machine (Root directory)

To specify an access mode for volumes that are two possible values:
- rw --> read-write (default)
- ro --> read-only (safer)

To allow Compose to manage the volume life cycle along the container life cycle, is recommended to use named volumes. 

>[!Example] Example - named volumes
>---
>```yaml
>services:
>  bookstack_db:
>    volumes:
>      - db_data:/var/lib/mysql
>volumes:
>  db_data:      
>```
>`/var/lib/mysql` --> persist any database data written inside the container and store it in the host machine. 

Advantage of using named volumes:
- during `up` or `start` compose will automatically copy volume data from old container to new containers and ensure that no data is lost.

port --> to expose a port that maps from the host machine to the Docker container. This is essential for accessing services from outside the Docker environment. The syntax for port mapping is `host_port_number:container_port_number`

>[!Example] Example - port mapping
>---
>```yaml
>services:
>  bookstack_db: 
>    ports:
>      - "3136:3136" # from port to port
>```
>It's recommend to put the mapping in quotes but not required unless the port number is below 60.

Compose provides utilities to enforce startup order automatically using the `depends_on` flag. Compose will start and stop services in dependency order. Services can have any number of dependencies and many services can share a single dependency. 

>[!Example] Example - dependency
>---
>```yaml
>services:
>  phpmyadmin:
>    image: phpmyadmin:5.2.2
>    ports:
>      - "8080:80"
>    depends_on:
>      - bookstack_db
>```
>It's recommend to put the mapping in quotes but not required unless the port number is below 60.

>[!note]
>Obs: modern versions of compose explicitly do not guarantee that dependent containers are running or are healthy, it only guarantees that they've been started.

networks --> This section lest define custom networks and connect services to them. This is useful for controlling communication between services.

tags --> defines a list of tags mappings that must be associated to the build image

>[!example] 
>```yaml
>tags:
>  - "myimage:mytag"
>  - "registry/username/myrepos:my-other-tag"
>```

>[!example] Example - npm tool
>```yaml
>services:
>  npm: 
>    build: ./
>    stdin_open: true
>    tty: true
>    volumes:
>      - ./:/app
>```

If you don't have a command or entry point at the end, then the command or entry point of the base image will be used if it has any.
###### <span style="color:#98971a">Dynamic Configurations </span>

Docker Compose provides a utility to start named subnet of services inside a single docker compose yaml file. Service profiles allows to put a docker service in one or more categories.

>[!example] Example - service profile
>```yaml
>services:
>  scheduler:
>    profiles: 
>      - scheduling_services
>  storefront:
>    profiles:
>      - storefront_services
>  database:
>```

A container with no profiles specified will be automatically included in the default profile --> it will run all the time with every service profile.

Once a default profile is specified in the configuration, docker compose will only apply to a service if its profile is explicit enabled. The `docker compose up` will run only services that are a part of the default profile.

To enable a non default profile:

```shell
docker compose --profile storefront-service up
```

A good case for multiple compose files is any situation where there are two distinct sets of desired behavior, that will never coincide. Example: separate compose override file for multiple environments. But having multiple compose files for different arts of a single system is not a good case.

By default, docker compose will read two configuration files, one named `docker-compose.yaml` (defaults), and another named `docker-composed.override.yaml`. The override file essentially inherits from the main configuration file.

Docker Compose will merge the two files together. During the merge, any field that can handle an array way of parameters like `dependen_on`, will include all values from both the primary and the override file. Any field that can handle only one value will five preference to that override. 

Obs: Any file paths reference in the override file must be relative to the primary configuration file.

The override file can be a partial or incomplete configuration. It can contain snippets of configurations specific only to what is being overwritten. One Docker Compose configuration can be easily shared between multiple project or repositories. It's also possible to have multiple override file in the same repository. Example: `docker-compose.local.yaml` and `docker-compose.staging.yaml`.

To run confirmation override files the `-f` flag must be used:

```shel
docker compose -f [primary file] -f [override file] [command]
```

```shel
docker compose -f docker-compose.yaml -f docker-compose.local.yaml up
```

If the Docker Compose configuration needs to have different behaviors in different environments, but it won't support configuration overrides  for every environment, a good alternative is using environment variables. 

Environment variables, although they can be used to substitute any part of the composed file to make ti more flexible in different environment.

To specify a default variable:
- empty string (automatic)
- inline in docker compose configuration
- in an external environment file (`.env`)
- requiring that the variable is not empty

>[!example] Example - environment variable
>```yaml
>services:
>  database:
>    image: "mysql:-${TAG}"
>```
>Obs: The curly braces are optional.

If the environment file has a different name, or it' it's outside the project directory, the `--env-file` flag allows to explicitly the file:

```shell
docker compose --env-file [path]
```

>[!note]
>Any environment that is set in the shell will always override a default value, whether that default is set inline or in an ENV file.

To require that an environment variable is present:

```yaml
image: "mysql:?Ooops TAG is a required"
```
##### <span style="color: #689d6a">Docker Commands</span>

- To <strong style="color: #b16286">run/start</strong> a container from an image <span style="color: #3588E9">--></span> <code style="color:#689d6a">docker run nginx</code>   
	- <code style="color:#689d6a">docker run redis:40</code> <span style="color: #3588E9">--></span> specifying a tag
	- <code style="color:#689d6a">-e</code> <span style="color: #3588E9">--></span> for environment variables
		- Ex: <code style="color:#689d6a">docker run -e APP_COLOR=pink webapp</code>
	- <code style="color:#689d6a">--link</code> <span style="color: #3588E9">--></span> option which can be used to link to containers together.
		- it creates an entry into the etc/hosts file on the voting app container, adding an entry with the host name redis with the internal IP of the redis container.
		- Ex: <code style="color:#689d6a">docker run -d --name=vote -p 500:80 --link redis:redis voting:app</code>
- To <strong style="color: #b16286">download</strong> the image <span style="color: #3588E9">--></span> <code style="color:#689d6a">docker pull nginx</code>
	- it pulls the image and stores on the host, it doesn't run the container.
- To <strong style="color: #b16286">upload</strong> an image <span style="color: #3588E9">--></span> <code style="color:#689d6a">docker push</code>
	- it sends a docker image to a public or private registry
- To <strong style="color: #b16286">attach back</strong> to the running container <span style="color: #3588E9">--></span> <code style="color:#689d6a">docker attach [id]</code>
- To <strong style="color: #b16286">create</strong> an image <span style="color: #3588E9">--></span> <code style="color:#689d6a">docker build -t webapp-color .</code>
	- <code style="color:#689d6a">-t</code> <span style="color: #3588E9">--></span> add a tag
	- <code style="color:#689d6a">.</code> <span style="color: #3588E9">--></span> indicates the current directory

Whenever a new image is created or an existing image is updated, it's pushed to the registry and every time anyone deploys this application, it is pulled from that registry.

Link is a command line option which can be used to link to container together

docker build -t image .

`docker run -d --name-vote -p 5000:80 --link redis:redis voting-app`
it creates an entrypoint on ETcd host file one the voting app container, adding and entry with the host name redis whot the internal IP of the redis container.

to attach the container 
`docker attach container_name`

`docker start -a container_name` --> to start in the attach mode

`docker run --name mycontainer myimage`

to remove a container automatically:
`docker run -p 3000:80 -d --rm ID`
Being able to run a container with the --rm flag
to automatically remove it when it's been stopped.

`docker exec -it contaier_name npm init`