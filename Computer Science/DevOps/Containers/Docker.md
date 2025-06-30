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

Best practices:
- use verified images --> use a container image scanner if using a verified image isn't possible. Example: Clair, Trivy or Dagba.
- avoid tagging as latest --> version tags can be overriudenm making rollback difficult 
- use non-root users --> it makes the contaienrs more secure.
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

images are templates / bluertns for container, multile containers can be created bases on one image.

With that, I mean that when you build an image,or when you rebuild it,
only the instructions where something changed,and all the instructions there after are re-evaluated.

<span style="color:#98971a">Docker images</span> consist on multiple layers, which are <strong>Read-Only</strong>, and each of these layers has an unique ID.

Every image has its own internal file system which is totally detached from the file system on the machine that docker is running. It's hidden away inside the Docker container. 

the image should be the template for the container.The image is not what you run in the end, you run a container based on an image.

Docker caches every instruction result,
and when you then rebuild an image,
it will use these cached results
if there is no need to run an instruction again.
And this is called a layer based architecture.

within the are one or more layers, each container snippets of the container's filesystem. layers are compressed archive that container set of files that make uo the containeer's file system along with some data about itself. These files are combined together to make up the folder that the container is given for its root file system,

images contain multiples laywers (1 insturctions = 1 layer) to optimze build spped (caching) and re-usability.

<span style="color: #d65d0e">Layers</span> are saved on disk only once and can be shared between images, which saves disk space and network bandwidth.

Each <span style="color: #d65d0e">layer</span> is only a set of differences from the layer before it, the layers are stacked on top of each other. When an image is run as a container a new <span style="color: #d65d0e">writable layer</span> (container layer) is added, which allows to make changes to the container.

the last layer is an image usually, but not always, contains instructions for configuring the container.

Each image will container a manifest at the root levels that provide more information about itself, including the relationship between its layers.
the container runtime uses manifests as guides for layers should be extracted and their containers configured.

Multiple containers are typically based on the same image, called <span style="color: #d65d0e">base image</span>. Changes made to the base image are actually stored in a new layer and don't the base layer.

images are either downloaded (docker pull) or created with a DOckerfile and docker build.

All changes made to the running container, are written to the container layer. But the files won't be persistent after the container is deleted. To write data in the writable layer of the container, Docker uses <span style="color: #d65d0e">storage drivers</span>.

Naming a Docker image: 
- <code style="color:#689d6a">[registry]/[repository]:[tag]</code> <span style="color: #3588E9">--></span> <code style="color:#689d6a">docker.io/ubuntu:18.04</code>

<span style="color: #d65d0e">Tags</span> are essentially <strong>aliases</strong>, an image can have multiple tags, but all points to the same source image. The tag <code style="color:#689d6a">latest</code> is a tag associated to the latest version of a software, which is governed by the authors of that software.

>[!note]
> Each version of the software can have multiple short and long tags associated with it

`docker build -t goals:latest .`


tha image name defines a grouo pf possible psefializaed, images. Example: node

A <span style="color: #d65d0e">Docker repository</span> within a registry is a collection of related Docker images with the same name but different tags. Each image is stored as a tag that can refer to different variations of an image.

>[!note]
>many companies choose to run their own registry within their own company to ensure that their data stays safe and private

<span style="color: #d65d0e">Dangling images</span> are <strong>layers that have no relationship</strong> to any tagged images.

To modify the <span style="color: #d65d0e">entrypoint</span> during runtime: 
- <code style="color:#689d6a">docker run --entrypoint sleep2.0 ubuntu-sleeper 10</code>

`docker image inspect ID` to inspect an image

to push image:
`docker push IMAGE_NAME`

to pull images:
`docker pull IMAGE_NAME`
###### <span style="color:#98971a">Container</span>

A container is a runnable instance of an image, it encapsulates everything an application needs to run.

Can be created, stopped, started or deleted using the Docker API or CLI.

Can connect to multiple networks, attach storage to the container, or create a new image based on its current state.

Is well isolated from other containers an its host machine.
that a Docker container is isolated.
It's isolated from our local environment.
And as a result, it also has its own internal network.

Containers are independent of the storage containers. Depending on the storage layer, in some cases it may run out of layers. Some storage have a limited number of layers.

Each container automatically gets a random ID and name created for it by Docker.

The Container ID uniquely identifies the container, it's used to refer to a certain container. When a container is started, if Docker doesn't return the Docker ID, then something is wrong. If there isn't an image on the machine, Docker will download the image.

All Docker container are nothing more than a process, looked from the perspective of the operating systems.

In Docker, the container starts with an init process and vanishes when this process exits.

To keep a long running container, its necessary to specify what the <span style="color: #d65d0e">Process ID 1</span> is. If that process is gone, the container will stop.

to copy file to a container
`docker cp local_folder/.  container_name:/path_inside_container`
`docker cp dummy/. brogin_vaughan:/test`

to copy a file from a container
`docker cp brogin_vaughan:/test local_folder`

naming and tagging a container
`docker run -p 3000:80 -d --rm --name goalsapp goals:latest`

use nont-root users when runnign container:
`docker run --rm -it --user somubody-else suspect-image:v1.0.1`
###### <span style="color:#98971a">Dockerfile</span>

The Dockerfile is a language for creating and describing docker container images. Dockerfile is the name of the lannguage, as well as the default name of thr file that Docker looks for when creaaing contaienr images. 

Every Dockerfile vonsist of a serr of commands (instructions), eahc on theur own line. The instruction is the first word of teh satement, every oher word after the inctruction is provided ot is as arguments.

>[!example] Example - Dockerfile
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

Docker process Docker file from top to bottom. Docker runs each Dockerilfe command in an "interminiadte container" (temporary container) and saves the reslts as ian image layer. These layers are joined together for form the mage as the Dockerfile is processed

The byproduct of the comabd that ran in te hcontainer is saved in to a layer. This layer is added t the the new image, which is goven t the intermidiate container crated by the next command of the DOckerfile. This process repeats until evry command inf Dockerfile is processed.

Each docker instruction on a Dockerfile creates a new layer in the image.

By default, all those commands will be executed in the working directory off your Docker container and image. And by default, that working directory is the root folder in that container file system.

Obs: Command like label, expose and entrypoint do not run in intermiadte containers.

Dockerfile commands
- <code style="color: #689d6a">FROM</code> <span style="color: #3588E9">--></span> defines the "base" image that the Dockerfile's image will be created from. It links the current image to the new image.
- <code style="color: #689d6a">RUN</code> <span style="color: #3588E9">--></span> executes arbitrary commands
- COPY --> 
- ADD --> 
- <code style="color: #689d6a">CMD</code> <span style="color: #3588E9">--></span> stands for command, it defines the program that will be run within the container when it starts. should be the last instructon
	- Obs: should only have 1 command instructions.
	- Different ways of specifying commands:
		- Shell form: `command1 param1`
		- JSON array: `["command", "param1"]` <span style="color: #3588E9">--></span> Obs: the first element should be the executable
- <code style="color: #689d6a">ENTRYPOINT</code> <span style="color: #3588E9">--></span> similar to the CMD instruction, it can specify the program that will run when the container starts. It appends commands typed on the terminal with `docker run` 
- WORKDIR --> set teh working direcoty inside teh container, tells Docker that all the subsequent commands will be executed from inside that folder.
- EXPOSE --> expose a certain port to the local system (machien running the container) It **documents** that a process in the container will expose this port, it'ß an optional command. 
- VOLUME --> maps a folder in the container to persist data
- USER --> to set the docker user

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

Ways to use FROM command:
select the "latest" tag of an image
```dockerfile
FROM ubuntu
```

select the tag of an image
```dockerfile
FROM ubuntu:kinetic
```

select the latest tag of an image and git it an alais (multi-stage build only)
```dockerfile
FROM ubuntu AS base
```

select the tag of an image and git it an alias name (multi-stage build only)
```dockerfile
# FROM $image:$tag AS $name
FROM ubuntu:kinetic AS base
```

When adding or coping  a file to the Docker container it's a good practice to use a sub folder instead of entering the root folder.

to restrict what is copied to the container, add a `.dockerignore` file to the project.
specify which folders and files, should not be copied by a copy instruction. just as using `.gitignore`

>[!example] Example  
>```dockerfile
>COPY . /app
>```
>All the files from the machine will be copied into the `.app` folder inside the container. If it doesn't exist the folder will be created in the image. 

COPY . ./ --> current working directory inside of our Docker container.

A Dockerfile is executed by the <code style="color:#689d6a">docker build</code> command. to create an image based on the instructions in this Dockerfile. 

>[!example] docker build
>```shell
>docker build .
>```
>When Docker finishes running the Dockerfile, the resulting image will be on the <span style="color: #d65d0e">local registry</span>.

Each step of running a Dockerfile is cached, Docker skips lines that haven't changed since the last build. dot here,
we tell Docker that the Dockerfile
will be in the same folder
as we're running this command in.

to run the container based of the dockerfile
docker run ID -p 3000:80

Every instruction represents a layer in your Dockerfile.
And an image is simply built up from multiple layers
based on these different instructions.

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

Multi-Stage builds allow you to have one Dockerfile, that define multiple build steps or setup steps, so called "stages" inside of that file.

Stages can copy results from each other, so we can have one stage to create the optimized files and another stage to serve them.

We can either build the entire Dockerfile going through all stages, step by step from top to bottom or we select individual stages up to which we wanna build, skipping all stages that would come after them

Now, with multistage builds, we just have to use "RUN" instead of command

>[!example] Example - multi stage build
>```dockerfile
>FROM node:14-alpine as build
>
>WORKDIR /app
>
>COPY package.json .
>
>RUN npm install 
>
>COPY .. 
>
>RUN npm run build
>
>FROM nginx:stable-alpine
>
>COPY --from=build /app/build /usr/share/nginx/html
>
>EXPOSE 80
>
>CMD ["nginx", "-g", "daemon off;"]
>```

After FROM build, you still need to specify the source path,
we're telling Docker that this copy will not refer to our local host project folder, but instead queue the file system from this build stage.
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

<code style="color:#689d6a">docker volume create</code> <span style="color: #3588E9">--></span> docker command to create a volume
docker volumes ls --> list all volumes managed

>[!example] example - docker volume create
>```shell
>docker volume create d_volume
>```
>creates a folder called d_volume under the `/var/lib/docker/volumes` directory.

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
>docker run \ --mount type,source=/data/mysql,target=var/lib/mysql mysql
>```
>The source is the location on the host and the target is the location on the container.

We use this bind Mount during development to reflect changes in our code, into running container instantly. Because if the container is running in production on a server, there is no connected source code, which updates while it's running.

bind mount:
`docker run -d -p 3000:80 --rm --name feedback-app -v feedback:app/feedback -v "home/user/guilherme/dev:/app" -v feddback-note:volumes`

`-v $(pwd):/app`

by default volumes are read write, --> the container is able to read data from there and write data to them.

to ensures that docker will now not be able to write into this folder or any of its sub-folders.

`docker run -d -p 3000:80 --rm --name feedback-app -v feedback:app/feedback -v "home/user/guilherme/dev:/app:ro" -v feddback-note:volumes`

Docker uses storage drivers to enable layered architecture. Some of the common storage drivers are: AUFS, ZFS, BTRFS, Device Mapper, Overlay, Overlay2. The selection of the storage driver depends on the underlying OS.

>[!info]
>Docker will choose the best storage driver available automatically based on the operating system.

How can I get my web server to access the database on the database container?

The right way to do it is to use the container name. All containers in a docker host can resolve each other with the name of the container. Docker has a built in DNS server that helps the containers to resolve each other using the container name.

How were the containers isolated within the host?
Docker uses network namespaces that creates a separate namespace for each container. It then uses virtual Ethernet pairs to connect containers together.

Obs: Bind mount shouldn't be used in Production!
##### <span style="color: #d79921">Docker Compose</span>

Docker compose is a tool for defining and running multi-container Docker applications. It allows to define an entire stack, including services, networks, and volumes with a single configuration file and then a set of orchestration commands to start all those services.

Docker Compose will not replace Docker files for custom images. Docker Compose works together with Docker files.

Docker Compose is really great for managing multiple containers on one and the same host.

>[!example] Example - 
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

<strong style="color:#98971a">Components:</strong>

services --> defines the various containers (services) that make up the application. Each service has a name, and under each service, parameters can be configured such as Docker image to use, environment variables, port to expose, volume to mount, etc.

image --> overrides the image name specified in the Dockerfile

volumes --> This section allows to define named volumes or bind mounts for the seervices. Volumes are used to persist data between contaienr restarts.

networks --> This section lest define custom networks and connect services to them. This is useful for controlling communication between services.

environment --> you can set environment variables for the services using 'environment' key. This is useful for configuring the applications dynamically.

port: This key allows to map ports from the host to the container. This is essential for accessing services from outside the Docker environment.

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

args --> passes bulid arguments to the build context. Useful for dynamically setting values during the build. 

>[!example] 
>```dockerfile
>ARG GIT_COMMIT
>RUN echo "Based on commit: $GIT_COMMIT"
>```
>```yaml
>build:
>  context: .
>  args:
>    GIT_COMMIT: cdc3b19
>```

tags --> defines a list of tags mappings that must be associated to the build image

>[!example] 
>```yaml
>tags:
>  - "myimage:mytag"
>  - "registry/username/myrepos:my-other-tag"
>```

normal flow

Dockerfile --> Docker Build Command --> Docker Image

Docker compose workflow

docker compose build --> build service
docker compose up --> start up service
-d --> background mode
docker compose down --> tear down service 
docker compose push --> push the images to docker hub
docker compose logs --> to view the logs of a service 
docker compose logs --tail=10 --> limit the container logs output
docker compose logs --follow --> follow the container log output
docker compose exec service_name shell --> shell into the container 
/bin/bash

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

`docker compsoe up -d --build server`
The `--build` option force docker compose to reevaluate the Docker files and rebuild images if required. orces docker-compose to go through the Docker files again and then recreate the images if something changed.


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
	- `-f` --> to keep listening the container
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