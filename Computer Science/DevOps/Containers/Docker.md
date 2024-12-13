Available since 2013, Docker Is an open platform (engine) written in Go, that allows to develop, deploy, test and run applications as containers. It uses Linux kernel's features to deliver functionality.

Docker isolates applications from infrastructure, including the hardware, operating systems and the container runtime. It uses the namespaces technology to provide an isolated workspace called "container" (containers are isolated from each other).

> The main purpose of Docker is to package and containerized applications and to ship them and to run them anywhere any time as many times is nedded.

Docker creates a set of namespaces for every container and each aspect runs in a separate namespace with access limited to that namespace.

<span style="color: #3588E9">--></span> <span style="color: #d65d0e">namespaces</span> is a <strong>feature of the Linux kernel</strong> that allows to provide complete network isolation to different processes on the system. It's similar in concept to what a <span style="color: #d65d0e">Hypervisor</span> does to provide the virtual resources to the Virtual Machine. They keep containers isolated until docker administrator allows containers to communicate over docker virtual network on the same host. With the namespaces isolation in Docker, operating systems and applications running in containers, feels like they have their own process tree.

namepsace isolation tecnique: Process ID namespaces

The processes running inside the container are in fact processes running on the underlying host. With process ID namespaces, each process can have multiple process IDs associated with it.

By default there is no restriction as to how much of a resource a container can use, and hence a container may end up utilizing all of the resources on the underlying host.

Docker primarily uses <span style="color: #d65d0e">cgroups</span> (control groups) to restrict the amount of hardware resources allocated to each container. This can be done by providing the --cpus option to the Docker run command. Example: docker run --cpus=.5ubuntu --> ensure that the container does not take up more than 50% of the host CPU at any given time. The same goes with memory: docker run --memory=100m ubuntu

Docker requires that virtualization to be enabled in the Bios, <span style="color: #d65d0e">VT-X</span> or <span style="color: #d65d0e">AMD-V</span>.

<span style="color: #3588E9">--></span> One of the goals of Docker is to make scripting distributed systems "easy".

- The <span style="color: #d65d0e">Docker Engine</span> which is the <strong style="color: #d79921">heart of Docker</strong>, is comprised of runtime and packing tools, and is required to be installed on the host that runs Docker. It's <strong>designed as client-server application</strong>, and it has these components: <span style="color:#98971a">Docker CLI</span> (docker client), <span style="color:#98971a">Dockerd</span> (docker daemon), <span style="color:#98971a">REST APIs</span>.
	- <span style="color:#98971a">Dockerd</span> <span style="color: #3588E9">--></span> it's the docker host server itself. The daemon listens for Docker API request or commands such as "docker run" and processes those commands. The daemon, is responsible for: build, run and distributes containers to the registry. Docker host includes and manages: images, containers, namespaces, networks, storage, plugins and add-on.
	- <span style="color:#98971a">Docker API</span> <span style="color: #3588E9">--></span> defines the interface that all programs use to talk to the daemon.
	- <span style="color:#98971a">Docker CLI</span> <span style="color: #3588E9">--></span> send instructions/commands to the Docker host server via command line interface (CLI) or through REST APIs. The Docker CLI can be used to communicate with local and remote host. The Docker CLI and the dockerd can run on the same system or connect the client to a remote docker daemon.
	- To use Docker CLI to work with remote docker engine, simply use the dash option (<code style="color:#689d6a">-H</code>) on the Docker command and specify the remote Docker engine address and a port <span style="color: #3588E9">--></span> <code style="color:#689d6a">docker -H=[remote-docer-engine]:[port]</code> <strong>Example:</strong> <code style="color:#689d6a">docker -H=10.123.2.1:2375 run nginx</code>
	- <span style="color: #3588E9">--></span> <span style="color:#98971a">docker daemon</span> can also communicate with other daemons to manage Docker services.
	- The Docker engine also utilizes <span style="color: #d65d0e">cgroups</span> for isolation, which are used for controlling container resources, primarily around CPU and memory, they provide resource isolation. Cgroups in Docker are strict Kernel requirements, which means that they need to be compatible.

Docker consist of multiple tools that are grouped toeghterL like Dockder CLI, Docker API, the build tools for buldign images.