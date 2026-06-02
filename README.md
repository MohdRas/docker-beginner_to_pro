# docker-beginner_to_pro
https://www.youtube.com/watch?v=RqTEHSBrYFw&amp;t=2886s

# Prerequisite
- Linux fundamentals - Basic Linux commands

# History & Motivation
- Docker helps to make local env as close as to production env where we are gonna deploy our application.
- setting up development env is easy. Just one command "docker compose up"
- earlier we need "deploment binary(JAR/WAR)", "dependencies", "configurations" to deploy an application. But with containers, just run this container image with these options.
# Technology overview
- containers
  - "lightweight", "standalone", "executable" package of software. This PACKAGE include "everything to run an application".
- Open Container Initiative - OCI
  - defines specification for containers.
    - Runtime specification
      - How you take an image and run it in a container ? 
    - Image specification
      - What format and metadata an image should include?
    - Distribution specification
      - How those images should be distributed.
      - registry, pulling & pushing of the images.
  - Docker, Google, VMWare, Microsoft & Dell has their "own implemention" of this "specification for containers".
- dockers
- Evaluation of Virtualization
  - https://medium.com/@dncgr8/vms-vs-container-191ed90c8019
  - https://erik-engheim.medium.com/containers-vs-vms-a80fe0f9a549
  - https://mkaschke.medium.com/virtual-machine-vm-vs-container-13ab51f4c177
  - https://medium.com/@marco.lindner/kernkonzepte-container-vs-vms-images-container-docker-engine-3eb1e5ac8067
  
  - Bare Metal
      - Bare Metal
  - Vitual Machine
    - each VM has its own Guest OS and it's Kernel through HYPERVISOR ( Type1 or Type2 )
    - Hypervisors can sit directly on top of the hardware (type-1) or on top of an OS (type-2)
    - multiple OS instances run on single host machine.
    - A Hypervisor is a software that imitates a particular piece of computer hardware or the entire computer.
    - Hypervisor allow the available physical resources to be partitioned into multiple virtual ones, called Virtual Machines (VMs).
    - The computer that runs a hypervisor is called the Host System(laptop, server, vm on ec2), and the VMs created and managed by the hypervisor are called the Guest Systems.
    - PROBLEM
          - each VM virtualizes an entire operating system and its underlying hardware.
  - Containers
    - All containers running on a host machine, share the OS kernel of the Host System, and only contain the application(s) and their libraries and dependencies.
    - each container uses Host OS and it's Kernel through Docker Engine.
    - Faster STARTUP, Less RESOURCES (lightweight)
    - Less ISOLATION as compared to VMs.
    - Host OS COMPATIBILITY ISSUE
        - Linux container will run on a Linux host, but not on a Windows host
    - Docker Engine
      - Docker Daemon (`dockerd`): Manages Docker objects such as containers, images, networks, and volumes.
      - REST API: Provides a programmable interface that allows various tools to interact with the Docker daemon.
      - CLI (`docker`): Provides users with a command-line interface for interacting with Docker.
      - Docker Compose : Allows you to define and run multi-container Docker applications.
      - Docker Swarm : A clustering and orchestration tool for Docker containers.
  - In summary, the reduced isolation and dependence on the host OS of containers bring both advantages in terms of performance and efficiency, as well as certain disadvantages, particularly in terms of security and portability. These factors must be considered when deciding whether to use containers or VMs for a particular application.
# Installation / Setup -  Hello World

# Using 3rd Party Containers

# Demo Application

# Building container images
- Dockerfile basics
- Dockerfile optimization
- Buildx + multi-architecture

# Container Registry

# Running Containers

# Docker networking
- https://www.youtube.com/watch?v=5grbXvV_DSk&t=564s
- https://www.youtube.com/watch?v=bKFMS5C4CG0
- docker creates 3 network driver (network types) automatically when we installed docker desktop or docker engine.
- 3 "drivers" or 3 "network types" are *bridge, none, host*
- *bridge, none, host* are pre-defined network and cannot be removed ( docker network rm <NETWORK_ID> )
- built-in DNS server run on IP 171.17.0.11
    - DNS server will resolve CONTAINER_NAME to IP_ADDRESS.
- docker network ls

		- NETWORK ID     NAME                DRIVER    SCOPE
		- e08c374b6b36   bridge              bridge    local
		- 56586189be5a   host                host      local
		- e486baa2c2fb   my-bridge-network   bridge    local
		- e4c236fa59cf   none                null      local

- docker network ls -f id=e08c374b6b36
	
		- NETWORK ID     NAME      DRIVER    SCOPE
		- e08c374b6b36   bridge    bridge    local

- docker network ls -f name=my-bridge-network
		
		- NETWORK ID     NAME                DRIVER    SCOPE
		- e486baa2c2fb   my-bridge-network   bridge    local

- docker network ls -f driver=bridge
	
		- NETWORK ID     NAME                DRIVER    SCOPE
		- e08c374b6b36   bridge              bridge    local
		- e486baa2c2fb   my-bridge-network   bridge    local

- docker network ls -f scope=local
		- NETWORK ID     NAME                DRIVER    SCOPE
		- e08c374b6b36   bridge              bridge    local
		- 56586189be5a   host                host      local
		- e486baa2c2fb   my-bridge-network   bridge    local
		- e4c236fa59cf   none                null      local
		
- docker network ls --filter type=builtin
		
		- NETWORK ID     NAME      DRIVER    SCOPE
		- e08c374b6b36   bridge    bridge    local
		- 56586189be5a   host      host      local
		- e4c236fa59cf   none      null      local



- docker network ls --filter type=custom
		
		- NETWORK ID     NAME                DRIVER    SCOPE
		- e486baa2c2fb   my-bridge-network   bridge    local


- docker network ls --filter scope=swarm
		
		- NETWORK ID   NAME      DRIVER    SCOPE


- docker network ls --no-trunc
		
		- NETWORK ID                                                         NAME                DRIVER    SCOPE
		- e08c374b6b3692f320a6c56d850c6e24eb87f05cec803898e40d3764eb4271e7   bridge              bridge    local
		- 56586189be5a4fc36517063f6e68bb567c0b26ee1a5be4fe70dbeb6536188d46   host                host      local
		- e486baa2c2fbdf72737444e74fe896643696c95801d71de4a03a681a44a5f065   my-bridge-network   bridge    local
		- e4c236fa59cf435489158a9ee8f2046a42c9c7aa7c9bac443d20c0f790728094   none                null      local

- **default bridge driver ( network type )**
  	- When you launch a new container with docker run it automatically connects to this bridge network. 
    - default network
        - IP 172.17.0.1 aasigned to interface "docker0"
        - IP 172.17.0.2 aasigned to first container
        - IP 172.17.0.3 assigned to second container
        - and so on...
        - till 172.17.0.16
    - docker run -d redis - The default bridge network (isolated).
  	- docker run -d -p 8080:80 redis - The default bridge network (isolated) + port binding
    - docker run -d --network bridge redis	 - The default bridge network (isolated).
    - 
    - to access these containers from outside, we need port binding.
        - exposing containers to the world using port binding.
        - docker run --rm -d -P 80:80 redis 
    - Container can be accessed in broswer only if port binding done.
        - http://IP_ADDRESS_OF_HOST_MACHINE:80
    - "docker inspect CONTAINER_ID" OR "docker inspect CONTAINER_NAME"
        - docker inspect redis
        - "redis" is the container name 
        - show "network" of a container. It will be only one.
    - "docker inspect NETWORK_ID" OR "docker inspect NETWORK_NAME"
        - docker inspect bridge 
        - "bridge" is the name of the network.
        - show "all containers" of a network. It can be multiple.
    - "ip a | grep docker0" command
        - Docker create interfaces for every bridge network
        - "docker0" is the interface of the default_bridge network. It IP is 172.17.0.1
    - containers communicate with each other using their internal IP address.
        - CONTAINER_1 - docker run --it -d --name redis-container redis
        - CONTAINER_2 - docker run --it -d --name nginx-container nginx
        - inside CONTAINER_1 (redis-container) IP 172.17.0.2
            - ping 172.17.0.3
            - ping google.com
            - "ip route" command
                - it will show "default via 172.17.0.1" which means routing via interface docker0 ( 172.17.0.1 )
       - inside CONTAINER_2 (nginx-container) IP 172.17.0.3
            - ping 172.17.0.2 
            - ping google.com
        - CHALLENGE
            - our application(container) want to connect to database (container).
            - after container restart, new IP address will be assiged, so communication using IPs is not correct.
        - SOLUTION
          - "user-defined" Bridge  
              - "user-defined" network is isolated from all other networks ( default, none & host). can't talk to them.
              - docker network create --driver bridge --subnet 182.8.x.x/16 custom-isolated-network
              - "custom-isolated-network" is the name of the user-defined network.
              - containers of this network communicate with each other using NAMES.
                  - mysql.connect(CONTAINER_NAME)
                  - CONTAINER_1 - docker run --it -d --name redis-container -net user-defined-network redis
                  - CONTAINER_2 - docker run --it -d --name nginx-container -net user-defined-network nginx
                  - inside CONTAINER_1 (redis-container)
                      - "ping nginx-container"
                          - possible due to DNS ( Container name to IP)
                      - ping google.com
                      - "ip route" command
                   - inside CONTAINER_2 (nginx-container)
                        - "ping redis-container"
                            - possible due to DNS ( Container name to IP)
                        - ping google.com 
                    - we can attach a network to a cotainer as part of the "docker run" command.
                    - docker run --net custom-isolated-network --it redis
                    - from inside container, we can execute "ping google.com" OR "ping HOST_MACHINE_IP_ADDRESS"
                    - but we cannot ping any IP address of the "default" bridge network due to isolation. ping 172.17.0.2 , won't work.
                    - we can also ping CONTAINER1 from CONTAINER2 or vice-versa. Both containers are attached to the same "user-defined" bridge network.
              - "docker network ls" command show all networks with details like NETWORK_ID, NAME, DRIVER & SCOPE
              - "ip a | NETWORK_ID" command
                  - show "network interface" details as each network has its own interface.
                  - IPs of "user-defined" bridge network is different than "default" bridge network.


- Host
	- Docker containers are isolated network‑wise by default.
When you run a container without extra flags it gets a bridge network (a private virtual NIC, NAT‑ed to the host).
--network host (or the older --net=host) **tells Docker not to create a separate network namespace for the container – it tells the container to share the network stack of the Docker Engine process (i.e. the host’s network namespace).**
	- No virtual Ethernet (eth0) is created inside the container.
	- The container sees the same interfaces, IP addresses, routing table, and firewall rules that the host (the Docker daemon) sees.
	- Ports are bound directly on the host’s IP; there is no Docker‑managed NAT or port‑mapping (-p).
	- The container can bind to any port the host can (including privileged ports < 1024).
	- The container can inspect/modify the host’s networking (e.g., run iptables, tcpdump).
	- Performance is slightly better because packets skip the Docker bridge/NAT hop.
 	- Linux kernel namespaces – By default Docker creates a new net namespace for each container (unshare(CLONE_NEWNET)).
	- With --network host, Docker skips the net namespace creation. The container runs in the same network namespace as the daemon (dockerd).
	- The container’s process tree still gets its own PID, mount, UTS, and cgroup namespaces (unless you also ask for --pid host, etc.).
	- Because the network namespace is shared, the container sees the same /proc/net, same /sys/class/net, and the same iptables tables as the host.
 	- docker run --network host <image>	Run container in host network mode (Linux containers only).
	- docker run --network bridge <image>	The default bridge network (isolated).
	- docker run -p 8080:80 <image>	Bridge mode + publish port 8080 on the host.
	- docker run --network none <image>	No network at all (isolated).
	- docker run --network container:<other>	Share the network namespace of another container (useful for side‑car patterns).
    - **docker run redis --network host**
    - ZERO isolation between container & host.
    - container wants to connect to other resources/services on the host
    - **this container is like any other application directly deployed on the host(VM) without the docker**. Just like a regular application on the host (VM).
    - **we don't need to expose the port.**
    - container uses the network of the host ( VM ).
    - **multiple container cannot be run on the same port.**
    - **Container can be accessed in broswer without port**
        - http://IP_ADDRESS_OF_HOST_MACHINE
- overlay network
    - create private overlay network across multiple hosts of a Docker swarm.
    - docker network --driver overlay --subnet 10.0.9.0/24 create my-overlay-network
    - create network across multiple host machines.
    - host1(container1, container2), host2(container3, container4), host3(container5, container6) are 3 different networks.
- ingress network
    -  
- None = docker run redis --network none
    - container is not attached to any network.
    - does not have any access to external network or any other container.
    - run in an isolated network.

# Docker Volumes

		-docker volume create	 - Create a volume
		-docker volume inspect	- Display detailed information on one or more volumes
		-docker volume ls	- List volumes
		-docker volume prune	- Remove unused local volumes
		-docker volume rm	- Remove one or more volumes
		-docker volume update	- Update a volume (cluster volumes only) 

- Volumes is used as data persistence for databases and other statefull applications.
- **The data of a container is stored in its virtual file system. It is not-persist. When we start a container, a FRESH virtual file system is created. Hence data lost.**

# Create Docker volume 
-  **docker volume create app-data**
- **app-data** is the name of the volume.
- **app-data** is the folder created at path (/var/lib/docker/volumes/ : real directory on the Docker host’s (WSL 2's) filesystem)
- full path : **/var/lib/docker/volumes/app-data/_data**
- Docker is managing **every volume on WSL 2 VM.**
- This volume is created with **local** Driver.

# List of Docker volumes
- Shows all volumes ( *anonymous, used & unused*)
- -  **docker volume ls**
	- DRIVER    VOLUME NAME
	- local     app-data

# List of Volumes based on "driver"
- 
- docker volume ls **-f driver=local**
	- DRIVER              VOLUME NAME
	- local               rosemary
	- local               tyler

# List of "unused" volumes
- In Docker Desktop
  - go to the Volumes view.
  - You can see the Status column, which shows whether a volume is "In use" by a container or "Unused".

- The dangling filter matches on all volumes not referenced by any containers.
  - docker volume ls **-f dangling=true**
  - The volumes coming from above command can be removed using **rm command**
  - docker volume rm <volume_name>

# List of volumes in "json" format
- docker volume ls **--format json**
				
				{"Availability":"N/A","Driver":"local","Group":"N/A","Labels":"","Links":"N/A","Mountpoint":"/var/lib/docker/volumes/app-data/_data","Name":"app-data","Scope":"local","Size":"N/A","Status":"N/A"}
				{"Availability":"N/A","Driver":"local","Group":"N/A","Labels":"","Links":"N/A","Mountpoint":"/var/lib/docker/volumes/hello/_data","Name":"hello","Scope":"local","Size":"N/A","Status":"N/A"}
				{"Availability":"N/A","Driver":"local","Group":"N/A","Labels":"","Links":"N/A","Mountpoint":"/var/lib/docker/volumes/volume1/_data","Name":"volume1","Scope":"local","Size":"N/A","Status":"N/A"}
				{"Availability":"N/A","Driver":"local","Group":"N/A","Labels":"","Links":"N/A","Mountpoint":"/var/lib/docker/volumes/volume2/_data","Name":"volume2","Scope":"local","Size":"N/A","Status":"N/A"}
  

# Inspect Docker volume
- **docker inspect app-data**

		[
		    {
		        "CreatedAt": "2026-05-25T12:51:44Z",
		        "Driver": "local",
		        "Labels": null,
		        "Mountpoint": "/var/lib/docker/volumes/app-data/_data",
		        "Name": "app-data",
		        "Options": null,
		        "Scope": "local"
		    }
		]


# Mount *Docker Volume* to a folder */data*
-  docker run -d -p 8086:8080 -v volume1:/data demo_my-app:1.1
-  docker run -d -p 8085:8080 --mount "source=volume1,target=/data" demo_my-app:1.1
-  Both does the same thing
-  *volume1* = the name of the volume created.
- *data* = it is the folder name inside container.
- docker debug <CONTAINER_ID> = we are now inside the container
- once we are inside container then type below command
- / # echo "This is critical production data" > /data/secret.txt
- / # exit

# Verify Data Persistence
-  **docker run --rm -it --name reader-container2 --mount "source=app-data,target=/data" alpine sh**
- / # cat /data/secret.txt
- This is critical production data

# Remove "anonymous" volumes
 - create **anonymous** volume
   - **docker volume create**
   - 042673d7d178724295daebea728edb835e20f157a90b1b7f9646d3bca4485d74  ( anonymous name)
 - **prune** anonymous volume
   - **docker volume prune**
   - WARNING! This will remove anonymous local volumes not used by at least one container.
   - Are you sure you want to continue? [y/N] y
   - Deleted Volumes:
   - 042673d7d178724295daebea728edb835e20f157a90b1b7f9646d3bca4485d74
   - Total reclaimed space: 0B

 
# Remove "unused" volumes
- **docker volume rm ( docker volume remove )**
- To remove unsed volumes.

	- If volume is **NOT used**
		- -  docker volume rm my-volume
		- my-volume
  
	- If volume is **used**
		- -  docker volume rm hello
		- **Error response from daemon: remove hello: volume is in use - [667acfd66ca9c28deab9ca460608c56da2933e94849af920da4f24d88186b11f]**

# Create Volume, Mount inside container and Write on this mount
- PS C:\Windows\System32> docker volume create **my-volume**
	- my-volume
	
- PS C:\Windows\System32> docker volume ls
	- DRIVER    VOLUME NAME
	- local     **my-volume**
	
- PS C:\Windows\System32> docker run -d -p 8080:8080 -v **my-volume**:/**folder-inside-container** my-app:1.1
	- c04f2e37c24dbc701ce87b55dca941bb51957838d6c573ba9689883874384f80
	
- PS C:\Windows\System32> docker ps
	- CONTAINER ID   IMAGE        COMMAND               CREATED          STATUS          PORTS                                         NAMES
	- c04f2e37c24d   my-app:1.1   "java -jar app.jar"   13 seconds ago   Up 13 seconds   0.0.0.0:8080->8080/tcp, [::]:8080->8080/tcp   confident_carson
	
- PS C:\Windows\System32> docker debug c04f2e37c24d
- root@c04f2e37c24d /app [confident_carson]
	- docker > ls
	- app.jar

- root@c04f2e37c24d /app [confident_carson]
	- docker > echo **"my first text file inside folder of a container"** > /**folder-inside-container/demo1.txt**
	
- root@c04f2e37c24d /app [confident_carson]
	- docker > ls
	- app.jar
	
- root@c04f2e37c24d /app [confident_carson]
	- docker > cd /
	
- root@c04f2e37c24d / [confident_carson]
	- docker > cd **folder-inside-container**
	
- root@c04f2e37c24d /folder-inside-container [confident_carson]
	- docker > ls
	- **demo1.txt**
- root@c04f2e37c24d /folder-inside-container [confident_carson]
	- docker > **cat demo1.txt**
	- **my first text file inside folder of a container**
- root@c04f2e37c24d /folder-inside-container [confident_carson]
	- docker > exit
	- exit
- PS C:\Windows\System32>
  
# Mount same volume inside another container & another folder and read it

- PS C:\Windows\System32> docker run -d -p 8081:8080 -v **my-volume**:/**another-folder** my-app:1.1
	- 3c1809c99bb83b8dad993c57dffc6a37c1a54ec39e56ef78e22afb8201389ea2
	
- PS C:\Windows\System32> docker ps
	- CONTAINER ID   IMAGE        COMMAND               CREATED          STATUS          PORTS                                         NAMES
	- 3c1809c99bb8   my-app:1.1   "java -jar app.jar"   9 seconds ago    Up 8 seconds    0.0.0.0:8081->8080/tcp, [::]:8081->8080/tcp   recursing_yalow
	- c04f2e37c24d   my-app:1.1   "java -jar app.jar"   11 minutes ago   Up 11 minutes   0.0.0.0:8080->8080/tcp, [::]:8080->8080/tcp   confident_carson
	
- PS C:\Windows\System32> docker debug 3c1809c99bb8
- root@3c1809c99bb8 /app [recursing_yalow]
	- docker > ls
	- app.jar
	
- root@3c1809c99bb8 /app [recursing_yalow]
	- docker > cd /
	
- root@3c1809c99bb8 / [recursing_yalow]
	- docker > ls
	- __cacert_entrypoint.sh  **another-folder**  app  bin  dev  etc  home  lib  media  mnt  nix  opt  proc  root  run  sbin  srv  sys  tmp  usr  var
	
- root@3c1809c99bb8 / [recursing_yalow]
	- docker > cd  **another-folder**
	
- root@3c1809c99bb8 /another-folder [recursing_yalow]
	- docker > ls
	- **demo1.txt**
	
- root@3c1809c99bb8 /another-folder [recursing_yalow]
	- docker > cat demo1.txt
	- **my first text file inside folder of a container**
	
- root@3c1809c99bb8 /another-folder [recursing_yalow]
	- docker > exit
	- exit
	
- PS C:\Windows\System32>
	



# Container Security

# Interacting with Docker Objects

# Development workflow

# Deploying Containers 
