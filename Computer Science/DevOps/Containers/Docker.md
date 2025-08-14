Available since 2013, Docker is an open platform (engine) written in Go, that allows to develop, deploy, test and run applications as containers. It uses Linux kernel's features to deliver functionality.

Docker isolates applications from infrastructure, including the hardware, operating systems and the container runtime. It uses the namespaces technology to provide an isolated workspace called "container" (containers are isolated from each other).

In container runtime, containers are compose of namespaces and control groups. Namespaces specify the resources that containers can see or access on a system. Whereas control groups specify how much of those resources containers can consume.

In container runtime, <span style="color: #d65d0e">namespaces</span> <strong style="color: #b16286">can be used to restrict what apps can do</strong> by adding or removing Linux capabilities from it.

<span style="color: #d65d0e">Capabilities</span> is a <strong style="color: #d79921">Linux Kernel feature</strong> that allows for fine-grained control over the privileges granted to processes and executable files. It allows applications to receive or not admin powers.

Docker creates a set of namespaces for every container and each aspect runs in a separate namespace with access limited to that namespace.

>[!info]
><span style="color: #d65d0e">Namespaces</span> is a <strong style="color: #d79921">feature of the Linux kernel</strong> that allows to provide complete network isolation to different processes on the system. It's similar in concept to what a <span style="color: #d65d0e">Hypervisor</span> does to provide the virtual resources to the Virtual Machine.

<strong style="color: #b16286">Namespaces keep containers isolated</strong> until docker administrator allows containers to communicate over docker virtual network on the same host. It specifies the resources that containers can see or access on a system.

The processes running inside the container are in fact processes running on the underlying host. With process ID namespaces, each process can have multiple process IDs associated with it.

By default there is no restriction as to how much of a resource a container can use, and hence a container may end up utilizing all of the resources on the underlying host.

Docker uses <span style="color: #d65d0e">cgroups</span> (control groups) to: 
1. Monitor and restrict CPU usage, or the amount of CPU time each container can take up.
2. Monitor and restrict network and disk bandwidth
3. Monitor and restrict memory consumption (more common)

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
###### <span style="color:#98971a">Logging</span>

By default Docker does not shows debug level jobs, but that can be changed by editing the docker daemon configuration. 

To <strong style="color: #b16286">enable</strong> debug:

```shell
sudo sh -c 'echo "{\"debug\": true}" > /etc/docker/daemon.json'
```

<strong style="color:#c6554f">Obs:</strong> restart the service after any changes on <span style="color:#98971a">dockerd</span>.

In case of Docker desktop, just type on the terminal

```shell
docker run -it --rm --privileged --pid=host guilhermeoliveira`
```

To <strong style="color: #b16286">return a full log</strong> of a container:

```shell
grep -i docker /var/log/syslog
```

The logging component of <span style="color:#98971a">systemd</span> is called <span style="color:#98971a">journald</span>, and it can be used for troubleshooting purposes. 

To <strong style="color: #b16286">debug</strong> docker in real-time:

```shell
sudo journalctl -f -u docker
```

To <strong style="color: #b16286">limit</strong> the last entries:

```shell
sudo journalctl -n 25
```

To <strong style="color: #b16286">show the output</strong> without a pager:

```shell
sudo journalctl --no-pager -u docker.service -n 25
```

When an application is running inside of a container, Docker uses logging drivers to capture data sent to streams (stdout, stderr, stdin). 

<span style="color: #d65d0e">Logging drivers</span> are <strong style="color: #b16286">program that forward data sent to standard out or standard error streams</strong> to somewhere else, like a folder on the disk or an online log-aggregation platform.

There are <strong style="color: #d79921">two ways</strong> trough which logging drivers can be configured:
- `--log-driver` <span style="color: #3588E9">--></span> flag that specifies the logging driver to use
- `--log-opts` <span style="color: #3588E9">--></span> flag that provides options for the logging driver.

To <strong style="color: #b16286">return information</strong> about the logging driver:

```shell
docker info | grep 'Logging Driver'
```

By default, retrieving logs from containers is a <strong style="color: #d79921">blocking operation</strong> <span style="color: #3588E9">--></span> the container and any applications within it will pause while the logging driver retrieve the logs. 

To <strong style="color: #b16286">avoid</strong> blocking operation:

```shell
--log-opts mode=nonblocking
```

>[!note]
>The `nonblocking` mode might cause data loss if containers exceed the space they've been given for log storage.

<strong style="color:#c6554f">Obs:</strong> by default the default logging driver stores logs on disk. Docker uses the json-file logging driver by default.

To <strong style="color: #b16286">disable</strong> logging:

```shell
docker run --name test-container --log-driver none my-image
```

To <strong style="color: #b16286">change</strong> the logging driver:

```shell
docker run --log-driver syslog --log-opt alpine
```
###### <span style="color:#98971a">Control Groups</span>

The usage of Control Groups makes easier to prevent busier, or larger containers from eating up all the system's resources and slowing other container down without having to carve up significant amount of memory like virtual machine do.

Control Groups allows to define rules like, this app can only use two CPUs, or this app can use no more than 128 megabytes of memory.

Most popular options for settings limits:
- `--cpus` <span style="color: #3588E9">--></span> sets maximum processor time
- `--memory` <span style="color: #3588E9">--></span> sets maximum amount of memory (in bytes)

These options use the CPU and memory control groups on the host system to enforce these limits.

Docker sets a default CPU period of 100 milliseconds, which is the same as setting the CPU period to 100.000, and CPU quota 140.000 in the processor.

>[!info]
>CPU control group allows the user to specify the maximum amount of processor time, a process within it can consume.

The `--cpus` is a permutation of:
- `--cpu-period` <span style="color: #3588E9">--></span> defines a period of time the operating system kernel should wait before giving the container processing time in microseconds.
- `--cpu-quota` <span style="color: #3588E9">--></span> defines the amount of processing time a container should have across all the CPUs on the system. 

To <strong style="color: #b16286">limit</strong> CPU usage:

```shell
docker run --rm --cpus 1.6 ubuntu --cpu 4 --timeout 5
```

To <strong style="color: #b16286">limit</strong> memory usage:

```shell
docker run --memory 2G --rm ubuntu
```
###### <span style="color:#98971a">Portainer</span>
 
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

The configuration options that determine how Docker behave:
- `/var/run/docker.sock` <span style="color: #3588E9">--></span> pipe between the Docker client and Docker Engine
- `/etc/docker/daemon.json` <span style="color: #3588E9">--></span> Docker Engine configuration (default)

The Docker engine uses namespaces to isolate what's happening in a  running container from the Operating System that hey are running. 

With namespaces, the Kernel resources, such as process ID, users ID, network, storage, can all be virtualized and share between the host Operating System and the container running on top of it.

The <span style="color:#98971a">Dockerd</span> it's the docker host server itself. The daemon listens for Docker API request or commands such as "docker run" and processes those commands.

The daemon, is responsible for: build, run and distributes containers to the registry. Docker host includes and manages: images, containers, namespaces, networks, storage, plugins and add-on.

To <strong style="color: #b16286">verify</strong> the daemon:

```shell
ps -ef | grep docker
```

Obs: the <span style="color:#98971a">docker daemon</span> can also communicate with other daemons to manage Docker services.

To <strong style="color: #b16286">show</strong> the <span style="color:#98971a">dockerd</span> documentation:

```shell
dockerd --help
```

Configuration options for <span style="color:#98971a">Dockerd</span>:
- `--config` <span style="color: #3588E9">--></span> Docker configuration file
- `--data-root` <span style="color: #3588E9">--></span> Folder to place all Docker objects into
- `--debug` <span style="color: #3588E9">--></span> Enables debug output in Docker Engine logs
- `--default-runtime` <span style="color: #3588E9">--></span> Default container runtime to use
- `--log-level` <span style="color: #3588E9">--></span> Configures the types of logs shown by Docker Engine
- `--insecure-registry` <span style="color: #3588E9">--></span> Image registries to connect insecurely to
- `--add-runtime` <span style="color: #3588E9">--></span> Add additional container runtimes, like <span style="color:#98971a">crun</span>

The configurations options can be stored in a JSON file (`daemon.json`)

>[!example] Example - Daemon configuration
>```json
>{
>  "insecure-registry": ["my-registry:5000", "another-registry"]
>  "log-level": "warn"
>}
>```

The <span style="color:#98971a">docker cli</span> sends instructions/commands to the Docker host server via command line interface (CLI) or through REST APIs. The Docker CLI can be used to communicate with local and remote host. The Docker CLI and the <span style="color:#98971a">Dockerd</span> can run on the same system or connect the client to a remote docker daemon.

By default the Docker client works in the root mode, to use as a normal user, the user needs to be added to the docker group.

```shell
sudo usermod -aG docker $USER
```

To use Docker CLI to work with remote docker engine, simply use `-h` option on the Docker command and specify the remote Docker engine address and a port.

```shell
docker -H=10.123.2.1:2375 run nginx
```
##### <span style="color: #689d6a">Docker Architecture</span>

Docker is <strong style="color: #b16286">based on client-server architecture</strong> which provides a complete application environment. Docker components includes the client, the host, and the registry.

<span style="color: #d65d0e">Docker hosts</span> are also called <strong style="color: #d79921">nodes</strong>, and they also include and manage: Images, Containers, Namespaces, Networks, Storage, Plugins and add-ons.

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

Docker stores all its data by default on this location: `/var/lib/docker`
###### <span style="color:#98971a">Container</span>

A Docker container <strong style="color: #b16286">is a runnable instance of an image</strong>, it encapsulates everything an application needs to run. It can be created, stopped, started or deleted using the Docker API or the Docker CLI.

<strong style="color: #b16286">All</strong> Docker container <strong style="color: #d79921">are nothing more than a process</strong>, looked from the perspective of the operating systems. When it starts the container automatically gets a random ID and a name created for it by Docker.

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

<strong style="color: #d79921">Containers are independent of the storage containers</strong>. Depending on the storage layer, in some cases it may run out of layers. Some storage have a limited number of layers.

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

Docker container have a minimal default set of capabilities, which can be changed with the `docker run` command.

Create a container that creates a file and changes its ownership:

```shell
docker run --entrypoint sh --rm alpine -c 'touch .tmp/file && chown 1001:1001 /tmp/file && echi "File permission changed" '
```

The `--cap-drop` option informs allow to remove a capability:

```shell
docker run --entrypoint sh --cap-drop --rm alpine -c 'touch .tmp/file && chown 1001:1001 /tmp/file && echi "Fiel permission changed" '
```

The capability that allows to change file ownership is called `CAP_CHOWN`. 

The `--cap-add` adds a capability: 

```shell
docker run --entrypoint sh --cap-add CHOWN --cap-add CAP_LEASE --rm alpine -c 'touch .tmp/file && chown 1001:1001 /tmp/file && echo "File permission changed"'
```

Obs: container can be assigned with multiple capabilities

>[!note]
>The `cap-add` option takes precedence over `cap-drop` option. 

To remove and then add capabilities:

```shell
docker run --entrypoint sh --cap-add CHOWN --cap-drop ALL --rm alpine -c 'touch .tmp/file && chown 1001:1001 /tmp/file && echo "File permission changed"'
```

The `--device` flag is used to give containers direct access to specific devices on the system. It's mostly useful if a container needs to use USB devices or GPU cards without granting it a full suite of other privileges.

The `--privileged` flag informs docker to treat a container as if it's a real process in the system. It can do everything and access anything.

```shell
docker run --entrypoint sh -it --privileged alpine
```

>[!info]
>To run docker in rootless mode, configures the docker engine so that it runs as a user other than root, this allows container to become root without being able to become root on the system.
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

<span style="color: #d65d0e">Storage drivers</span> define how layers are stored on disk and represented to containers. In other words, storage drivers are responsible for decompressing layers into a directory structure, and presenting them to a container as a fake route directory. 

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

Whenever a new image is created or an existing image is updated, it's pushed to the registry and every time anyone deploys this application, it is pulled from that registry.

>[!note]
>Many companies choose to run their own registry within their own company to ensure that their data stays safe and private

Naming a Docker image: 
- <code style="color:#689d6a">[registry]/[repository]:[tag]</code> <span style="color: #3588E9">--></span> <code style="color:#689d6a">docker.io/ubuntu:18.04</code>

To <strong style="color: #b16286">pull</strong> (download) an image:

```shell
docker pull [image_name]
```

To <strong style="color: #b16286">push</strong> an image:

```shell
docker push [image_name]
```

To <strong style="color: #b16286">search</strong> for images in Docker Hub:

```shell
docker search python
```

The `--filter` option allows to <strong style="color: #b16286">filter</strong> search results:

```shell
docker search --filter is-official=true python
```

To <strong style="color: #b16286">log</strong> into Docker Hub:

```shell
docker login
```

>[!info]
>Docker saves the credentials for Docker Hub in the home directory, so that it can easily login in the feature.

To <strong style="color: #b16286">push</strong> the image into a registry:

```shell
docker image tag my-server username/my-server:0.0.1
```

```shell
docker push username/my-server:0.0.1
```

To <strong style="color: #b16286">pull</strong> the image from registry:

```shell
docker pull username/my-server:0.0.1
```

The image can also be pulled using the IP address

```shell
docker pull 192.168.56.100:5000/my-server
```

To <strong style="color: #b16286">run</strong> the container from the private registry:

```shell
docker run -d -p 5000:5000 --name registry registry:2
```
###### <span style="color:#98971a">Network</span>

Docker provides the ability to <strong style="color: #b16286">access network ports within the container</strong> with something called <strong style="color: #d79921">port biding</strong> <span style="color: #3588E9">--></span> allows Docker to take a port on the host machine, and map it to a port within the container. 

To <strong style="color: #b16286">map ports</strong> for the container:

>[!example] Example - port biding
>```shell
>docker run -d --name jenkins-server -p 8080:80 jenkins
>```
>`[outside:inside]` <span style="color: #3588E9">--></span> outside of the container, and inside of container
>
>`8080:80` <span style="color: #3588E9">--></span> the traffic on the the `8080` port of the Docker host will be routed to the `80` port inside the container

<strong style="color:#c6554f">Obs:</strong> The same port can't be mapped on the Docker host more than once.

network are used for the isolated container communication.
Within a Docker network, all containers can communicate with each other and IPs are automatically resolved.

All containers attached to this network by default, and they get an internal IP address usually in the range 172.17.0.0 series. The containers can access each other using this internal IP if required

>[!info]
>Every docker container gets an IP assigned by default, but it's an internal IP.

To <strong style="color: #b16286">associate</strong> a container with any network:

```shell
docker run ubuntu --network=host
```

The `network` flag can also be used to add multiple containers into the same network.

>[!example] Example - Docker network
>```shell
>docker run -d --name mongodb --network favorites-net mongo
>
>docker run --name favorites --network favorites-net -f --rm -p 3000:3000 favorites-node
>```

To allow communication between the applications running in a container to the host achine machine just use the address `host.docker.internal`.

Almost every <strong style="color: #d79921">container engine's networking model is based</strong> on plug-ins. These plug-ins describe how these packets get routed to containers.  Third party network drivers can be installed through network plugins, which can be found on Docker Hub or through GitHub.

Some plug-ins will send these packets to containers through virtual network card in the local machine. Other plug-ins might give container "real network cards" that work with the network card on the local machine to receive packets appropriately.

<span style="color:#98971a">Weaveworks Weave Net</span> plugin is the most popular network plugin. It allows to create virtual networks for containers that span multiple hosts. It comes with additional features, like service discovery and network policies. 

<strong style="color: #b16286">Every container</strong> <strong style="color: #d79921">uses the bridge docker network</strong> by default. It connects docker containers to a virtual bridge network installed on the host machine.

>[!info]
>A <strong style="color: #d65d0e">bridge network</strong> is a <strong style="color: #d79921">virtual network device</strong> that <strong style="color: #b16286">connects multiple networks together</strong> into a single network. Bridge networks are useful for taking traffic from a real network adapter and forwarding it to virtual network adapters.

<span style="color: #d65d0e">Bridge drivers</span> isolate through network namespace unsharing and iptables.

The net namespace allows container within it to get their very own network stack that's isolated from the network stack on the host system, including network adapters.

Additionally, docker uses IP tables rules to ensure that bridges are isolated from each other.

>[!note]
>When Docker is installed, it creates three networks automatically: Bridge, None, Host. Bridge is the default network a container gets attached to.

Sub command for working with networks:

```shell
docker network
```

To <strong style="color: #b16286">create</strong> an internal network:

```shell
docker network create [network_name]
```

To <strong style="color: #b16286">set</strong> the network driver:

```shell
docker network create --driver bridge [network]
```

The `--network` option allows to join a container to a different network.

```shell
docker container create -it --name container-a --entrypoint sh     --network network-a curlimages/curl
```

<strong style="color:#c6554f">Obs:</strong> Container on the default bridge need to know each other IP addresses.

Every bridge network will have a gateway IP address and a subnet expressed in the classless inter domain routing notation or CIDR.

<strong style="color: #b16286">By default</strong> containers in different bridge networks <strong style="color: #b16286">cannot</strong> talk to each other. To change it is by joining one of the containers to the containers network. 

Another way to communicate containers is by publishing a port of the container and map it to a port on the host machine.

<strong style="color: #d79921">Port publishing</strong> uses IP tables, a rules engine for filtering linux packets to "rewrite" packets destined for a container's IP address and a port on the host machine. This allows to connect a container trough the container's bridge network gateway on the host machine.

Obs: Only ports that are free on the host machine can be mapped.

The `--publish` option allows port publishing:

```shell
docker container create -it --name container-a --entrypoint sh     --network network-a --publish 8080:80 curlimages/curl
```

Obs: In a Mac or Windows machine the Docker Engine ir running inside of the VM. The ports will be mapped to ports within the VM.

>[!info]
>Docker Desktop works around this by using a background program called VPNKit to proxy connections between the host and containers within its VM. Lima does the same thing but with SSH tunnels.

Another way to access the containers externally is to associate the container to the <strong style="color: #d65d0e">host network</strong>. This takes out any network isolation between the Docker host and the Docker container.

Containers that use the host driver do not get the network namespaces unshared to them. They also do not get allocated virtual network adapters. 

Containers that use host mode networking get their packets like any other process on the system.

<strong style="color: white">Benefits</strong> of <strong style="color: #d65d0e">host network</strong>:
- slightly faster than bridge networks
- allows connections to multiple container ports from the outside
- containers are accessible from the host IP instead "virtual" IP <span style="color: #3588E9">--></span> advantageous for applications that are sensitive to NAT like VPN software

```shell
docker run --rm --network host -it --entrypoint sh curlimage/curl
```

The <strong style="color: #d65d0e">null network</strong> driver is used to create containers without any external networking capabilities. These containers will not be able to communicate with other container or any network or with the outside world <span style="color: #3588E9">--></span> <strong style="color: #b16286">isolated network</strong>.

Containers connected to a network backed with a null driver will get a loop back interface, so that it can connect to itself trough the special 127.0.0.1 IP address and localhost DNS label. The <strong style="color: #d65d0e">none network</strong> is <strong style="color: #b16286">provided by default</strong>, but the user can create its own none network.

```shell
docker run --rm --network none --entrypoint sh curlimages/curl 
```

>[!note]
>The <strong style="color: #d79921">null network driver doesn't disable networking entirely</strong>. It only disables external networking outside of the container. Networked applications running within the container will still be able to talk to each other at localhost.

<strong style="color: white">Advanced Network Drivers:</strong>
- <strong style="color: #d65d0e">macvlan</strong> <span style="color: #3588E9">--></span> give containers real IP addresses on the network.
- <strong style="color: #d65d0e">ipvlan</strong> <span style="color: #3588E9">--></span> give containers real IP addresses on the network.
- <strong style="color: #d65d0e">overlay</strong> <span style="color: #3588E9">--></span> creates a container network that spans multiple nodes

<strong style="color: #d65d0e">macvlan</strong> and  <strong style="color: #d65d0e">ipvlan</strong> are both useful for containers running applications that need to discover other devices on the network, like music servers or home automation software, or secure high performance applications that needs to bypass a network bridge without having access to all of te host's network interface.

Both drivers work by binding containers to specific network card on the host running docker engine

>[!note]
>Docker does nos provides networks that use the macvlan or ipvlan driver by default. 

<strong style="color: white">Differences</strong> between <strong style="color: #d65d0e">macvlan</strong> and <strong style="color: #d65d0e">ipvlan</strong>:
- macvlan networks give container individual MAC addresses, which can lead to a network degradation
- ipvlan gives containers the same MAC address and using a network driver on the host to handle traffic
- ipvlan can operate in L2 and L3 mode, but in L2 mode ipvlan behaves almost exactly like macvlan, except everything going through a single MAC address.

Obs: In L3 all routing is done by the Docker host instead of working through a network interface default gateway.

To create macvlan or ipvlan networks:

```shell
docker network create -d macvlan --subnet SUBNET -o INTERFACE 
--gateway GATEWAY
```

The `-o` option must be used if the macvlan driver is being used or if the ipvlan driver in L2 mode is being used too/.

The `--gateway` option is optional for L3-mode ipvlan networks.

>[!example] Example - macvlan driver
>```shell
>docker network create -d macvlan --subnet 192.168.1.0/24 -o eth0   
>--gateway 192.168.1.1 my-net
>```

The `--aux-address` option can be use to give Docker a list of IP addresses to exclude from allocation.

The `--ip-range` option allow to specify and IP address range. It informa Docker to allocate IP addresses from a range of addresses. The range must be provided in CIDR format. 

>[!example] Example
>```shell
>docker network create -d macvlan --subnet 192.168.1.0/24 -o eth0   
>--gateway 192.168.1.1 --aux-address "host=192.168.1.2" my-net
>```
>```shell
>docker network create -d macvlan --subnet 192.168.1.0/24 -o eth0 
>--gateway 192.168.1.1 --ip-range 192.168.1.64/26 my-net
>```
>aux can be specified multiple times for every address to be excluded. 
>
>Each option requires a label of the host or device being excluded. 
>

The <strong style="color: #b16286">goal</strong> of an <strong style="color: #d65d0e">overlay</strong> network is to <strong style="color: #d79921">make container running on multiple machines,</strong> and potentially multiple networks, appear as if they are on a single network. 

Most <strong style="color: #d65d0e">overlay</strong> networks use three things:
- a network tunnel
- a virtual network interfaces on each node
- an agent (daemon) running on each node 

The agents are <strong style="color: #b16286">responsible</strong> for <strong style="color: #d79921">sending network packets from containers</strong> through virtual network interfaces installed by the overlay. 

The virtual networks interfaces than wrap each packet into a bigger packet that gets sent through the tunnel to its destination. Usually, the packets are encrypted in transit within the tunnel to prevent outsiders from figuring out what's being sent within it or through it.

Once it arrives there, the original packet is retrieved from the bigger packet and sent to the container through the overlay's virtual network interface.

Technologies that overlay uses to establish the secure tunnel, <span style="color:#98971a">Virtual Extensible LAN</span> or <span style="color:#98971a">vxlan</span>, and <span style="color:#98971a">Wire Guard</span> are the most popular choices.
###### <span style="color:#98971a">Storage</span>

<strong style="color: #b16286">Everything</strong> created within a container <strong style="color: #d79921">stays within the container</strong>. Once the container stops, the data gets deleted with it.

The <strong style="color: #d65d0e">volume mounting</strong> feature can be used to solve the issue related to data persistence. Docker allows to <strong style="color: #b16286">map</strong> a <strong style="color: #d79921">folder on the host machine to a folder in the container</strong>, which is called a <strong style="color: #d65d0e">bind mount</strong>.

>[!info]
>The data inside a bind mount is not stored outside the container, if the container is removed, the data will be lost.

A mount is useful to share code or configurations files between the host machine and the container during development or testing.

The `-v` or `--volume` option allows to map a folder. 

```shell
docker run --rm -v "source:destination:[ro]"
```

<strong style="color:#c6554f">Obs:</strong> outside is the folder on the host machine to be used, and inside is the folder within the container to map it to. The `ro` indicate the file access permissions, which in this case is readonly.

>[!example] Example - volume mounting
>```shell
>docker run --rm --entrypoint sh-v /tmp/container:/tmp ubuntu -c "echo 'Hello there.' > /tmp/file && /tmp/file"
>```

>[!note]
>If a file mapped in the host machine (source) does not exist, it will be mapped as a directory within the container.

In some system the <strong style="color: #d79921">source</strong> might need to be an absolute directory (full path). <strong style="color: #d79921">Destination</strong> will be created as a directory if it doesn't exist!

Ways of deal with the full (absolute) path:  `$PWD` or `realpath` tool.

To <strong style="color: #b16286">use</strong> `$PWD` way:

```shell
docker run --rm -v $PWD/stuff:/stuff alpine
```

To ensure that docker will now not be able to write into the folder or any of its sub-folders.

```shell
docker run -d -p 3000:80 --rm --name feedback-app -v feedback:app/feedback -v "home/user/guilherme/dev:/app:ro" -v feddback-note:volumes
```

Another way to mount is by using the `--mount` option:

```shell
docker run --mount "type=bind,src=<volume-name>,dst=<mount-path>,readonly,volume-opt"
```

The `--mount` allows to specify exactly how Docker should mount the volume. it does so by accepting five key values pairs separated by commas. 

>[!example] Example - mount option
>```shell
>docker run -i -t --rm --mount 'type=volume,source=test,destination=/test' alpine
>```
>type <span style="color: #3588E9">--></span> specifies the type of volume, that can be bind, tnpfs, or volume.

>[!info]
>The `volume-opt` key can be specified more than once, and the values provided can vary from driver to driver. The values: `type`, `source`, and `destinaion` are mandatory when using mount. 

Bind mount two advanced configuration parameters: `bind-propagation` and `selinux-label`. 
- `bind-propagation`: configures how sub-mount are presented
- `selinux-label`: configures whether mount can be shared with other containers

<strong style="color: #d65d0e">Bind mount</strong> is used during development to reflect changes in the code, into running container instantly. Because if the container is running in production on a server, there is no connected source code, which updates while it's running. 

Bind mount is also great if data of an app isn't very intensive.

<strong style="color: white">Uses Cases</strong> - <strong style="color: #d65d0e">bind mount</strong>:
- Hot reloading an application within a container while changing code from outside of it
- Backing up and restoring Docker volumes
- Faster one-off containers (from con jobs or other scheduled tasks)

---

The file systems represented to containers are actually unified sets of folders behind the scenes. Volumes works similarly, when a volume is mounted into a container, Docker maps a folder into a mount point within the container. 

<strong style="color: #d65d0e">Volumes</strong> allows to safely handle data coming into and out of containers. A volume is a <strong style="color: #d79921">directory on the host machine that is accessible to a container</strong>. 

<strong style="color: #d65d0e">Volumes</strong> are a good option for persisting data across different container, which can be used to store data from a database outside the container. It's recommended using volumes if the container is dealing with large files.

When a volume is used, a new directory is created within Docker's storage directory on the host machine, and Docker manages that directory's contents.

When a Docker volume is used, the data inside it is not stored in the container's file system, but in the host machine's file system <span style="color: #3588E9">--></span> the data in a volume persists even if the container is deleted or recreated.

A container can write data into a volume and read data from it. By default, volumes are <strong style="color: #b16286">read write</strong> <span style="color: #3588E9">--></span> the container is able to read data from there and write data to them.

To <strong style="color: #b16286">create</strong> a volume:

```shell
docker volume create [volume_name]
```

When a volume is created, it's stored within a directory on the Docker host.

The `-d` flag can be used to change the volume driver and the `-o` flag to specify additional configuration options to the volume driver.

>[!note]
>Obs: By default when a volume is created, docker will store the volume at `/var/lib/docker/volumes`

To <strong style="color: #b16286">list</strong> all available volumes:

```shell
docker volume ls
```

To <strong style="color: #b16286">inspect</strong> a volume:

```shell
docker volume inspect [volume_name]
```

To <strong style="color: #b16286">mount</strong> a volume:

```shell
docker run --mount type=volume,src=<volume-name>,dst=<mount-path>
```

```shell
docker run --volume <volume-name>:<mount-path>
```

When a volume is mounted into a container, this directory is what's mounted into the container.

To <strong style="color: #b16286">remove</strong> a volume:

```shell
docker volume rm [volume_name] # or docker volume prune
```

To <strong style="color: #b16286">remove</strong> all volumes:

```shell
docker system prune --volumes -f
```

To backup the volume:

>[!example] Volume - backup
>```shell
>docker run --rm -v $PWD:/target -v dir-important:/backup alpine tar cvzf /target/backup.tar -C /backup .
>```
>The first `-v` bind mount the current directory inside the container, and the second `-v` mount the volume to backup.

After creating the `.tar` compressed file it's important to confirm the backups. The best way is to extract the file and compose a file check sums, to ensure that the data hasn't been modified or corrupted.

To restore the backup:

>[!example] Volume - restore
>```shell
>docker volume create dir-restore
>
>docker run --rm -v $PWD:/target -v dir-restore:/restore alpine tar xvf /target/backup.tar -C /restore .
>
># Confirm the restore 
>docker run --rm -v dir-restore:/restore alpine cat /restore/README
>```

A defined path in the container is mapped to the create volume / mount.

---

<strong style="color: white">Types</strong> of volumes: 
- <strong style="color: #d65d0e">anonymous volumes</strong>  <span style="color: #3588E9">--></span> created specifically for a single container, attach to a container, can be used to save (temporary) data inside the container
- <strong style="color: #d65d0e">named volumes</strong> <span style="color: #3588E9">--></span> volumes persist even if the container is shut down, as the folders in the hard drive. good for data which should be persistent but which it doesn't need to be edit directly. 

To automatically remove an <strong style="color: #d65d0e">anonymous volumes</strong> it must use the `--rm` option during the start of a container. If the container is started without that option, the anonymous volume would **NOT be removed ** even if you remove the container (with `docker rm ...`). 

To <strong style="color: #b16286">create</strong> an anonymous volume:

```shell
docker run -v /app/data/ ...
```

To <strong style="color: #b16286">create</strong> a named volume:

```shell
docker run -v data:/app/data
```

---

Volumes present folders, shares, or block devices to container through volume drives. <strong style="color: #d65d0e">Volume drivers</strong> define <strong style="color: #d79921">how volumes are created and managed by containers</strong>.

Docker uses the local volume driver by default. The local driver simply creates a directory within Docker system directory, and mounts it in the container like a virtual disk or sorts.

>[!info]
>The local driver supports NFS, CIFS, and block devices. Volumes drivers can be installed to create many different kinds of volumes.
###### <span style="color:#98971a">Multi-app images</span>

use an entrypoint script that execute other program in the background, then run with `docker run --init` --> configurdd the container to run th entrypont script whithin a process supervisor called tini --> watchs every process runnign in the container and makes sure that signal are passed coreeclty to them.

install and configure systemd in the image

use amore sophiscated process supervisor, like s6-overlay --> it does the same job as Tini, but it also allows users to express multiple service in convenient directory structure. 

docker run -e APP_USER=Guilherme --rm test=app
###### <span style="color:#98971a">Registry</span>

The <strong style="color: #d65d0e">image registry</strong> is a <strong style="color: #d79921">web server that serves container images</strong>. The difference between a regular web server from an image registry is how the images are laid out.  

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

To log into the local registry:

```shell
docker login localhost:5000
```

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

<strong style="color:#c6554f">Obs:</strong> The `-f` flag can be used to keep listening the container.

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

The <code style="color:#689d6a">-e</code> option allows to add environment variables to a container:

```shell
docker run -e APP_COLOR=pink webapp
```

The <code style="color:#689d6a">--link</code> option can be used to link to containers together.

```shell
docker run -d --name-vote -p 5000:80 --link redis:redis voting-app
```

On the example above, the `--link` option creates an entrypoint on ETcd host file on the voting app container, adding and entry with the host name redis with the internal IP of the redis container.

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

To <strong style="color: #b16286">format</strong> the output:

```shell
docker inspect test-container --format '{{.ID}}'
```

The use of `--format` flag when inspecting any container it's interesting, because it can be used with identifiers to minimize the information returned.  

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

The <strong style="color: #d65d0e">Dockerfile</strong> is a <strong style="color: #b16286">language</strong> <strong style="color: #d79921">for creating and describing docker container images</strong>. Dockerfile is the name of the language, as well as the default name of the file that Docker looks for when creating container images. 

<strong style="color: #b16286">Every</strong> Dockerfile <strong style="color: #d79921">consist of a set of commands</strong> (instructions), each on their own line. The instruction is the first word of the statement, every other word after the instruction is provided to is as arguments.

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

<strong style="color:#c6554f">Obs:</strong> Command like `LABEL`, `EXPOSE` and `ENTRYPOINT` do not run in intermediate containers.

To <strong style="color: #b16286">build</strong> the image from a Dockerfile:

```shell
docker build .
```

To <strong style="color: #b16286">build</strong> from a different Dockerfile:

```shell
docker build -f server.Dockerfile . # -f or --file option
```

The `--force-rm` option allows to remove any intermediate containers that exist, even if the build is unsuccessful.

```shell
docker build --force-rm=true .
```

The `--rm=true` option can also be used in case of unsuccessful build. The intermediate container will not be removed. This allows for debugging the last intermediate container or committing it as an intermediate image.

```shell
docker build --rm=true .
```

>[!note]
>The context is simply the folder containing files that Docker will include in the image.

The `--no-cache` option can be used to skip the cache and rebuilt the entire image. It's useful in case the installation depends on external resources.

```shell
docker build --no-cache .
```

If the Dockerfile is elsewhere the path to it must be informed:

```shell
docker build ~/Dockerfiles/ubuntu/
```

>[!info]
>When Docker finishes running the Dockerfile, the resulting image will be on the <strong style="color: #d65d0e">local registry</strong>. And each step of running a Dockerfile is cached, Docker skips lines that haven't changed since the last build

If the name of the source image is defined without a tag, the default tag will be used, which is latest. When there's no tag defined, Docker assumes that the image that's being created is the latest version of the images in the repository.

To <strong style="color: #b16286">build</strong> an image with a tag:

```shell
docker build -t my-webapp:v1 .
```

When creating a new version of an image, the "build" command must be used to rebuild the image with a new image ID <span style="color: #3588E9">--></span> good for keeping each version separate.

```shell
docker build --no-cache -t my-webapp:v2 .
```

To <strong style="color: #b16286">run</strong> a container based on a Dockerfile:

```shell
docker run container_id -p 3000:80
```

In case the build output shows a warning saying that "legacy build is deprecated", consider using BuildKit, Docker's improved image builder. 

<strong style="color: #d65d0e">BuildKit</strong> <strong style="color: #b16286">provides</strong> <strong style="color: #d79921">improved performance and additional helpful features</strong> over the legacy builder that ships with Docker. The "build" command use it underneath the hood for version of Docker Desktop published after 2023. 

To <strong style="color: #b16286">use</strong> BuildKit:

```shell
docker buildx build [options]
```

Docker Builds gives to the user more options with what can be done with images that it provides. 

```shell
docker buildx build -t my-image --load .
```

The `--load` is a shortcut that tells BuildKit to build the image and load it into Docker when it's done.

<strong style="color:#c6554f">Obs:</strong> the "buildx" command creates build container or builders when it's run for the first time.

<strong style="color: white">BuildKit's features:</strong>
- use exportes <span style="color: #3588E9">--></span> give the user more control over the image that it produces
- automatically push images into image registries after the build
- save images into the host machine as tarball files
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

Using <strong style="color: #b16286">wildcards</strong> on arguments:

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

<strong style="color:white">Shell Form:</strong>
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

<strong style="color:white">Exec Form:</strong>
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

<code style="color: #689d6a">ARG</code> <span style="color: #3588E9">--></span> defines build arguments, which are variables provided at build time.

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

<code style="color: #689d6a">ENV</code> <span style="color: #3588E9">--></span> defines environment variables that containers started from an image should receive. 

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

Differences between ENV and ARG
- ENV variables are defined for every container started from an image; ARG variables are only used during runtime.
- ARGs are set at build time, ENVs are set at run time --> it can't be override through docker build, environment variables can only be override is by using the `-e` or `--env` flag with docker run. 

Similarities between  ENV and ARG
- Both ENV and ARG can only be expanded within Run commands
- ENVs and ARGs used by RUN commands must precede the RUN commands that reference them

<code style="color: #689d6a">LABEL</code> <span style="color: #3588E9">--></span> allows to document the images by adding metadata to them. Accepts a key-value pair. The most popular LABEL in Docker image is the maintainer.

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

<code style="color: #689d6a">WORKDIR</span> <span style="color: #3588E9">--></span> sets a working directory from RUN commands within the Dockerfile and/or container create from the image. The last WORKDIR will be used by containers.

```dockerfile
WORKDIR /app
```

<code style="color: #689d6a">USER</span> <span style="color: #3588E9">--></span> sets the Linux or Windows user to be used for RUN command and/or container. 
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

<code style="color: #689d6a">EXPOSE</span> <span style="color: #3588E9">--></span> documents network ports that containers created from the image should expose at runtime. It only accepts as arguments the port number.
- By default it assumes TCP ports
- Does not automatically expose ports
- Useful for documentation; completely optional

```dockerfile
EXPOSE 8080
```

<code style="color: #689d6a">VOLUME</span> <span style="color: #3588E9">--></span> maps a folder in the container to persist data

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

Docker supports build-time arguments and runtime environment variables. Arguments allows to set flexible bits of data in a Dockerfile which can be used to pluck different values into certain Dockerfile instructions.

Use `-e` or `--env` to <strong style="color: #b16286">set</strong> environment variables inside a Dockerfile: 

```shell
docker run -d --rm -p 3000:8000 -e PORT=8000 --name feedback-app
```

To <strong style="color: #b16286">specify</strong> a file that contains an environment variable:

```shell
docker run -d --rm -p 3000:8000 --env-file ./.env --name feedback-app
```

Use `--build-arg` to <strong style="color: #b16286">build</strong> another environment with a different value: 

```shell
docker build -t feedback-node:dev --build-arg DEFAULT_PORT=8000 .
```

>[!note]
>Arguments and environment variables allows to create more flexible images and containers because it doesn't have to hard-code everything into these containers and images. Instead they can be set dynamically when building an image or even running a container. 
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
##### <span style="color: #689d6a">Docker in Docker</span>

Docker in docker is <strong style="color: #d79921">managing containers created by Docker within a docker container</strong>. 

<strong style="color: #d65d0e">Docker in Docker</strong> is useful when an app needs to interact with the Docker engine itself, like running containerized test suites, creating/managing containers from within containerized apps, or emulating entire platforms as containers.

Ways to create a container that creates other containers:
- install Docker engine within the container 
- mount Docker's UNIX docket on the container to a file within a container and install just a Docker client

<strong style="color: white">Issues</strong> with Docker Engine in Docker:
- relies on version 2 of cgroup driver
- overlay filesystem incompatibilities
- containers inaccessible outside of parent containers

The <strong style="color: #b16286">best alternative</strong> to use Docker "in" Docker is by <strong style="color: #d79921">configuring the container to communicate the existing Docker engine</strong> and create containers from it. This is done by bind mounting the UNIX socket used by the Docker engine to the container <span style="color: #3588E9">--></span> it will create container directly from where the Docker engine is running.

<strong style="color:#c6554f">Obs:</strong> it uses the context of the machine that's running the Docker engine, not the context of the container.

To do pure Docker "in" Docker, its best to do with <strong style="color: #d65d0e">sysbox</strong>, which is <strong style="color: #d79921">container runtime</strong> that makes it really easy to run Docker within Docker. It does this through a special runtime that handles all of the details of creating and managing container within a container.

>[!example] Docker in Docker
>```shell
># Create the container 
>docker run --rm -v /var/run/docker.sock:/var/run/docker.sock --entrypoint bash -i -t my-image
>
># Check the communication with docker engine
>curl --unix-socket /var/run/docker.sock http://anything/containers/json
>
># Install docker client
>curl -L get.docker.io | bash
>
># Create a new container
>docker run --rm my-image
>```

<strong style="color: white">Limitations:</strong>
- shared containers, volumes, networks and other resources managed by the Docker engine can be seen
- the resources can be used from within the container
- mounted volumes <span style="color: #3588E9">--></span>  it mounts the file as a directory on the host

To solve the issue related to shared resources is to use <strong style="color: #d65d0e">Sysbox</strong> as the Docker "in" Docker approach. This <strong style="color: #d79921">keeps everything isolated</strong> within its own Docker engine while still being managed by the Docker engine on the virtual machine.

To solve the issue related to bind mount is by using Docker volumes, which will  share the file within the container as a file within the child container. 

<strong style="color: white">Solve</strong> the bind volume issue:

<strong style="color: #b16286">Create</strong> the volume:

```shell
docker volume create temp
```

<strong style="color: #b16286">Create</strong> child container:

```shell
docker container create -v temp:/tmp alpine
```

<strong style="color: #b16286">Copy</strong> the directory "/app" into the volume:

```shell
docker cp /app [container_id]:/tmp/app
```

 <strong style="color: #b16286">Start</strong> the child container:

```shell
docker run --rm -it -v temp:/tmp alpine
```
##### <span style="color: #689d6a">Docker Compose</span>

<strong style="color: #d65d0e">Docker compose</strong> is a <strong style="color: #d79921">tool for defining and running multi-container</strong> Docker applications. It allows to define an entire stack, including services, networks, and volumes with a single configuration file and then a set of orchestration commands to start all those services.

It <strong style="color: #d79921">can document a system as a runnable configuration file</strong> <span style="color: #3588E9">--></span> <strong style="color: #d65d0e">compose manifest</strong>. Compose <strong style="color: #b16286">does not add</strong> any <strong style="color: #d79921">functionality do the docker ecosystem</strong>, but it does make the existing functionality significantly easier to use; and it also works together with Dockerfiles.

<strong style="color: white">Normal Workflow:</strong>
- Dockerfile <span style="color: #3588E9">---></span> Docker Build Command <span style="color: #3588E9">---></span> Docker Image

To get started using Docker Compose, the first step is to create a configuration file (compose manifest) inside the application directory. 

>[!note]
>Every docker compose configuration must be in a yaml file, and be saved under the file name "docker-compose.yaml"

>[!example] Example - compose manifest
>```yaml
>services:  # specify all the containers for the app
>  bookstack: # service name (can be any name)
>    image: lscr.io/linuxserver/bookstack:version-
>    container_name: bookstack
>```

<strong style="color: #b16286">Most common</strong> commands for <strong style="color: #d79921">managing the lifecycle</strong> of Docker services: <strong style="color: #d65d0e">up, down, stop, restart.</strong>

<strong style="color: #d79921">Compose is a declarative tool, and it's self-document</strong>. It was designed as a tool for a single hosted server. It's well suited for local  development, staging server, continuous integration testing environment, and it's great for managing multiple containers on the same host.

<strong style="color:#c6554f">Obs:</strong> It's  <strong style="color: #d65d0e">not designed</strong> <strong style="color: #d79921">for distributed systems</strong> and has no tooling for containers across multiple hosts. Compose was designed for non-production environments only. 
###### <span style="color:#98971a">Compose Commands</span>

To <strong style="color: #b16286">build</strong> each defined services:

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

To <strong style="color: #b16286">start up</strong> only one service:

```shell
docker compose up -d bookstack 
```

To <strong style="color: #b16286">stop</strong> and <strong style="color: #b16286">delete</strong> all running containers:

```shell
docker compose down
```

The `--volumes` will automatically delete any named volumes:

```shell
docker compose down --volumes
```

To <strong style="color: #b16286">free up</strong> memory:

```shell
docker compose stop
```

To <strong style="color: #b16286">start</strong> and <strong style="color: #b16286">restart</strong> all running containers:

```shell
docker compose restart
```

To <strong style="color: #b16286">validade</strong> the docker compose file:

```shell
docker compose config
```

<strong style="color:#c6554f">Obs:</strong> Thy syntax for using docker compose if it's installed as a part of docker engine is `docker compose`, but in case it's installed as a standalone binary, it must the following syntax: `docker-compose`.

To <strong style="color: #b16286">push</strong> the images to docker hub:

```shell
docker compose push
```

To <strong style="color: #b16286">view</strong> the logs of a service:

```shell
docker compose logs
```

To <strong style="color: #b16286">limit</strong> the container logs output:

```shell
docker compose logs --tail=10
```

To <strong style="color: #b16286">follow</strong> the container log output:

```shell
docker compose logs --follow
```

To <strong style="color: #b16286">shell</strong> into the container:

```shell
docker compose exec [service_name] shell
```
###### <span style="color:#98971a">Compose Components</span>

 <strong style="color: #d65d0e">services</strong> <span style="color: #3588E9">--></span> defines the various containers (services) that make up the application. Each service has a name, and under each service, parameters can be configured such as Docker image to use, environment variables, port to expose, volume to mount, etc.

>[!example] Example - service
>```yaml
>services:
>  bookstack:
>    ...
>  bookstack_db:
>    ...

<strong style="color:#c6554f">Obs:</strong> Docker Compose services can be named anything. They are intended to be human readable and ideally should be meaningful. 

<strong style="color: #d65d0e">image</strong> <span style="color: #3588E9">--></span> defines the value to be used for the service, it also overrides the image name specified in the Dockerfile.

>[!example] Example - image
>```yaml
>services:
>  bookstack_db:
>    image: mariadb:lts
>```
>Docker Compose will tech the MariaDB image automatically from Docker Hub.

<strong style="color: #d65d0e">command:</strong> This key lets override the default command for the environment. This is useful when you need o specify how the container should start.

```yaml
command: npm start
```

<strong style="color: #d65d0e">build/context:</strong> It defines either a path do a directory containing a Dockerfile, or a URL to a git repository.

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

dockerfile <span style="color: #3588E9">--></span> specifies an altervative Dockerfile for the build

>[!example] 
>```yaml
>build:
>  context: .
>  dockerfile: Dockerfile.dev
>```

<strong style="color: #d65d0e">Environment variables</strong> at Docker are <strong style="color: #d79921">visible from inside the running container</strong>. The most common and simple use case a Docker environment variable if for specifying thing like a current runtime configuration such as dev or prod.

<strong style="color: #d65d0e">Build arguments</strong> are a <strong style="color: #b16286">type of</strong> <strong style="color: #d79921">environment variable that are available to docker only at build time</strong>, but not inside the container. They are useful for specifying a version for a certain build tool or cloud platform configuration.

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
>args <span style="color: #3588E9">--></span> attribute to pass build arguments to the build context. Useful for dynamically setting values during the build. 
>
>environment <span style="color: #3588E9">--></span> to set environment variables for the service. Useful for configuring the applications dynamically

>[!info]
>The most common use for docker environment variable is for specifying things like a current runtime configuration, such as dev or test.

Running `export runtime_env=dev` on the host machine and leaving the value out from the Docker Compose configuration will have the same effect as specifying inside the file. 

<strong style="color:#c6554f">Obs:</strong> use environment files if the lost of variable gets too long.

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

<strong style="color: #d65d0e">volumes</strong> <span style="color: #3588E9">--></span> This section allows to define named volumes or bind mounts for the services. Volumes are used to persist data between container restarts.

>[!Example] Example - volumes
>---
>```yaml
>services:
>  bookstack_db:
>    volumes:
>      - ./db_data:/var/lib/mysql:ro
>      - ./db_config:/etc/mysql/conf.d
>```
>`./db_data` <span style="color: #3588E9">--></span> source
>`/var/lib/mysql` <span style="color: #3588E9">--></span> target

Compose conforms to Bash standards for specifying a directory path. 
- `./` <span style="color: #3588E9">--></span> current directory
- `../` <span style="color: #3588E9">--></span> parent directory, one level above the compose configuration file
- `/` <span style="color: #3588E9">--></span> absolute path on the host machine (Root directory)

To specify an access mode for volumes that are two possible values:
- rw <span style="color: #3588E9">--></span> read-write (default)
- ro <span style="color: #3588E9">--></span> read-only (safer)

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

<strong style="color: #d65d0e">port</strong> <span style="color: #3588E9">--></span> to expose a port that maps from the host machine to the Docker container. This is essential for accessing services from outside the Docker environment. The syntax for port mapping is `host_port_number:container_port_number`

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

<strong style="color: #d65d0e">networks</strong> <span style="color: #3588E9">--></span> This section lest define custom networks and connect services to them. This is useful for controlling communication between services.

<strong style="color: #d65d0e">tags</strong> <span style="color: #3588E9">--></span> defines a list of tags mappings that must be associated to the build image

>[!example] Example - tags
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

A container with no profiles specified will be automatically included in the default profile <span style="color: #3588E9">--></span> it will run all the time with every service profile.

Once a default profile is specified in the configuration, docker compose will only apply to a service if its profile is explicit enabled. The `docker compose up` will run only services that are a part of the default profile.

To enable a non default profile:

```shell
docker compose --profile storefront-service up
```

A good case for multiple compose files is any situation where there are two distinct sets of desired behavior, that will never coincide. Example: separate compose override file for multiple environments. But having multiple compose files for different arts of a single system is not a good case.

By default, docker compose will read two configuration files, one named `docker-compose.yaml` (defaults), and another named `docker-composed.override.yaml`. The override file essentially inherits from the main configuration file.

Docker Compose will merge the two files together. During the merge, any field that can handle an array way of parameters like `dependen_on`, will include all values from both the primary and the override file. Any field that can handle only one value will five preference to that override. 

<strong style="color:#c6554f">Obs:</strong> Any file paths reference in the override file must be relative to the primary configuration file.

The override file can be a partial or incomplete configuration. It can contain snippets of configurations specific only to what is being overwritten. One Docker Compose configuration can be easily shared between multiple project or repositories. It's also possible to have multiple override file in the same repository. Example: `docker-compose.local.yaml` and `docker-compose.staging.yaml`.

The `-f` or `--file` flag are used to run configuration files overrides, it stands for file.

```shell
docker compose -f [primary file] -f [override file] [command]
```

```shell
docker compose -f docker-compose.yaml up
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
><strong style="color:#c6554f">Obs:</strong> The curly braces are optional.

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