# docker-beginner_to_pro
https://www.youtube.com/watch?v=RqTEHSBrYFw&amp;t=2886s

# Prerequisite
- Linux fundamentals - Basic Linux commands

# History & Motivation
- Docker helps to make **local env as close as to production env** where we are gonna deploy our application.
- setting up development env is easy. Just one command "docker compose up"
- earlier we need "deploment binary(JAR/WAR)", "dependencies", "configurations" to deploy an application. But with containers, just run this container image with these options.
# Technology overview
- container image
  - "lightweight", "standalone", "executable" package of software. This PACKAGE include **"everything to run an application".**
- Open Container Initiative - OCI
  - OCI is defines **open industry standards around what a container is and how should it run**
  - Docker, Google, VMWare, Microsoft & Dell has their "own implemention" of this "specification for containers".
  - defines specification for containers.
    - **Image** specification
      - What **format and metadata**, an image should include?
    - **Runtime** specification
      - How you **take an image and run** it in a container ? 
    - **Distribution** specification
      - How those images should be distributed ( **registry, pulling & pushing** of the images.)
    
- **docker is a specific implementaion of this specification.**
- Evaluation of Virtualization
  - https://medium.com/@dncgr8/vms-vs-container-191ed90c8019
  - https://erik-engheim.medium.com/containers-vs-vms-a80fe0f9a549
  - https://mkaschke.medium.com/virtual-machine-vm-vs-container-13ab51f4c177
  - https://medium.com/@marco.lindner/kernkonzepte-container-vs-vms-images-container-docker-engine-3eb1e5ac8067
  
  - **Bare Metal**
    - running applications directly on hardware/host itself.
	- slow start up & shut down speed ( in minutes)
	- **Dependency hell**
			- Both applications share the same binaries/libraries. Issue if both applications need different dependencies or some dependecies are not compatible with each other. This is known as **dependency hell**.


					|----------------------------------------------------------------------------|                                                                            |
					|          ----------------------------------------------------              |
					|          |                          |                         |            |
					|          |    Application #1        |  Application #2         |            |
					|          ---------------------------|-------------------------             |
					|                                                                            |
					|          ----------------------------------------------------              |
					|          |                Binaries /Libraries                |             |
					|          |                to run applications                |             |
					|          ----------------------------------------------------              |
					|                                                                            |
					|          ----------------------------------------------------              |
					|          |                     os                            |             |
					|          ----------------------------------------------------              |
					|          														             |
					|                                                                            |
					|          |----------------------------------------------------|            |
					|          |                  hardware                          |            |
					|          |----------------------------------------------------|            |
					|                                                                            | 
					|                                                                            |
					|                 Physical machine ( bare metal) / HOST                      |
					|-----------------------------------------------------------------------------


				

  - **Vitual Machine**
  	- Hypervisor 
			-  some combination of software/hardware that allows us to carve up the pool of physical resources ( cpu, ram, rom, networking etc) to smaller pool that allows us to install our system on to.
    - each VM has its own **Guest OS and it's Kernel** through HYPERVISOR ( Type1 or Type2 )
    - **Hypervisors can sit directly on top of the hardware (type-1) or on top of an OS (type-2)**
    - Type 1 = Hyper-v (microsoft), vSphere ( vmware) and aws nitro system.
	- Type 2 = VirtualBox - to create virtual machines on your laptop.
    - multiple OS instances run on single host machine.
    - **A Hypervisor is a software that imitates a particular piece of computer hardware or the entire computer.**
    - **Hypervisor allow the available physical resources to be partitioned into multiple virtual ones, called Virtual Machines (VMs).**
    - The computer that runs a hypervisor is called the Host System(laptop, server, vm on ec2), and the VMs created and managed by the hypervisor are called the Guest Systems.
    - PROBLEM
          - each VM virtualizes an entire operating system and its underlying hardware.



				|------------------------------------------------------------------------------------| 
				|																			         |
				|																			         |
				|                       VM2                        VM2                               |
				|          |---------------------------|       |----------------------|              |
				|          |            |              |      |           |           |              |
				|          |  App#1     |    app #2    |      |  App #3   | App #4    |              |
				|          |------------|--------------|      |-----------|---------- |              |
				|          |                           |      |                       |              |
						   |        Binaries           |      |     Binaries          |              |
				|          |        Libraries          |      |     Libraries         |              |
				|          |---------------------------|      |---------------------- |              |
				|          |                           |      |                       |              |
				|          |         OS                |      |      OS               |              |
				|          |---------------------------|      |---------------------- |              |
				|          |                           |      |                       |              |
				|		   |                           |      |                       |              |
				|		   |    Virtual hardware       |      | Virtual hardware      |              |
				|		   |                           |      |                       |              |
				|		   |-----------------------------     |---------------------- |              |
				|                                                                                    |
				|                                                                                    |
				|                                                                                    |
				|                                                                                    |
				|          |--------------------------------------------------- |                    |
				|          |                     Hypervisor                     |                    |
				|          |--------------------------------------------------- |                    |
				|          														|                    |
				|          |--------------------------------------------------- |                    |
				|          |                  OS - if type 2 hypervisor         |                    |
				|          |--------------------------------------------------- |                    |
				|                                                               |                    |
				|          |--------------------------------------------------- |                    |
				|          |                  hardware                          |                    |
				|          |--------------------------------------------------- |                    |
				|                                                                                    |
				|                                                                                    |
				|                           Physical machine                                         |
				|------------------------------------------------------------------------------------|


  - **Containers**
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
- *bridge, none, host* are pre-defined network and cannot be removed ( docker network rm <NETWORK_ID> )
- You can connect multiple containers to the same network. Once connected, the containers can communicate using only another container's IP address or name.
	- Docker’s DNS service (the internal 127.0.0.11 resolver) is only enabled on user‑defined networks (networks you create with docker network create).
 	- containers connected to default bridge network cannot communicate to each other via container name but can do via IP.
  		- ping container_name  - will fail from inside of another container for default bridge network
		- ping IP  - will work from inside of another container for default bridge network
- built-in DNS server run on IP 171.17.0.11
    - DNS server will resolve CONTAINER_NAME to IP_ADDRESS.
 
- builtin driver networks
	- automatically created when we installed docker desktop or docker engine.
	- cannot be removed.
	- docker network ls **-f type=builtin** 
	- bridge, none, host ( these are the names of the network)
 	- the "bridge" network corresponds to the **docker0** bridge that Docker Engine has traditionally relied on.
      
- custom driver networks
	- created by the user.
	- multiples can be created & can be removed.
	- we can only create **"bridge"** driver type networks. The **"host"** and **"null"** driver type networks cannnot be created.
	- docker network ls **-f type=custom** 
	- On a bridge network you can only create a single subnet: **docker network create --driver=bridge --subnet=192.168.0.0/16 br0**


 docker network create --driver=bridge --subnet=192.168.0.0/16 br0


# docker network create
- Creates a new network.
- docker creates 3 driver networks (bridge, none, host) automatically when we installed docker desktop or docker engine.
- *bridge, none, host* are pre-defined network and cannot be removed ( docker network rm <NETWORK_ID> )
- Only custom 
- If you don't specify the --driver option, the command automatically creates a bridge network for you.
- Only **custom created bridge driver networks** can be deleted.
- **bridge driver network** which was created by the user
- docker network create my-firs-default-bridge-net

			5894fa1e2881c2943915ef564d5725886f350b21ba42b178feb5c6cb1e13dbb6
   
- docker network create **--driver=host** my-first-host-net

			Error response from daemon: only one instance of "host" network is allowed

- docker network create **--driver=null** my-first-null-net
			
			Error response from daemon: only one instance of "null" network is allowed

- docker network create **--driver=bridge** my-first-host-net
			
			4fbaeaf2c6de76bc54d08513c9f16b4ae24bbd3c37f4d13f2fd7cfe8b9f371de
  
- docker network ls

  			NETWORK ID     NAME                         DRIVER    SCOPE
			e08c374b6b36   bridge                       bridge    local  ===============> "bridge" driver networks = multiple allowed
			56586189be5a   host                         host      local  ===============> "host" driver network = only one allowed
			5894fa1e2881   my-firs-default-bridge-net   bridge    local
			41fa6346ff55   my-first-net                 bridge    local
			e4c236fa59cf   none                         null      local   ===============> "null" driver network = only one allowed

  
# Docker network list
- docker network ls
	- Lists all the networks the Engine **daemon** knows about ( **custom & builtin** )

			NETWORK ID     NAME                DRIVER    SCOPE
			e08c374b6b36   bridge              bridge    local
			56586189be5a   host                host      local
			e486baa2c2fb   my-bridge-network   bridge    local
			e4c236fa59cf   none                null      local

- docker network ls **-f id=e08c374b6b36**
	- filter based on id=<NETWORK_ID>.
	
			NETWORK ID     NAME      DRIVER    SCOPE
			e08c374b6b36   bridge    bridge    local

- docker network ls **-f name=my-bridge-network**
	- filter based on name=<NETWORK_NAME>.
		
			NETWORK ID     NAME                DRIVER    SCOPE
			e486baa2c2fb   my-bridge-network   bridge    local

- docker network ls **-f driver=bridge**
	- filter based on driver=bridge.
   
			NETWORK ID     NAME                DRIVER    SCOPE
			e08c374b6b36   bridge              bridge    local
			e486baa2c2fb   my-bridge-network   bridge    local	
		
- docker network ls **-f type=builtin**
	- shows only builtin network drivers.
	- filter based on type=builtin.
    
			NETWORK ID     NAME      DRIVER    SCOPE
			e08c374b6b36   bridge    bridge    local
			56586189be5a   host      host      local
			e4c236fa59cf   none      null      local


- docker network ls **-f type=custom**
	- shows only custom (user-defined) network drivers.
	- filter based on type=custom.
	   
			NETWORK ID     NAME                DRIVER    SCOPE
			e486baa2c2fb   my-bridge-network   bridge    local


- docker network ls **-f scope=swarm**
	- filter based on scope=swarm.
   
			NETWORK ID   NAME      DRIVER    SCOPE

- docker network ls **-f scope=local**
	- filter based on scope=local.

	  		NETWORK ID     NAME                DRIVER    SCOPE
			e08c374b6b36   bridge              bridge    local
			56586189be5a   host                host      local
			e486baa2c2fb   my-bridge-network   bridge    local
			e4c236fa59cf   none                null      local


- docker network ls **--no-trunc**
	- **--no-trunc** to show full network id.
		
			NETWORK ID                                                         NAME                DRIVER    SCOPE
			e08c374b6b3692f320a6c56d850c6e24eb87f05cec803898e40d3764eb4271e7   bridge              bridge    local
			56586189be5a4fc36517063f6e68bb567c0b26ee1a5be4fe70dbeb6536188d46   host                host      local
			e486baa2c2fbdf72737444e74fe896643696c95801d71de4a03a681a44a5f065   my-bridge-network   bridge    local
			e4c236fa59cf435489158a9ee8f2046a42c9c7aa7c9bac443d20c0f790728094   none                null      local

# Docker network - remove unused **custom** networks
- docker network prune
	- This will remove all custom networks not used by at least one container.

			docker network prune
			WARNING! This will remove all custom networks not used by at least one container.
			Are you sure you want to continue? [y/N] y
			Deleted Networks:
			my-bridge-network
   
# Docker network - remove **custom** networks
- docker network rm <NETWORK_NAME_OR_ID>
	- **To remove a network, you must first disconnect any containers connected to it.**

- docker network rm my-network

  				Error response from daemon: error while removing network: network my-network has active endpoints (name:"nervous_carver" id:"8eea1c6a8be5")

- docker network disconnect my-network nervous_carver
	- my-network = name of network
	- nervous_carver = name of container
	
	
- docker network ls


				NETWORK ID     NAME         DRIVER    SCOPE
				e08c374b6b36   bridge       bridge    local
				56586189be5a   host         host      local
				94dd8b11c124   my-network   bridge    local
				e4c236fa59cf   none         null      local
	
	
- docker inspect my-network
	- see **"Containers": {},** ==>> Means no container to network

					[
						{
							"Name": "my-network",
							"Containers": {},
							"Status": {
								"IPAM": {
									"Subnets": {
										"172.18.0.0/16": {
											"IPsInUse": 3,
											"DynamicIPsAvailable": 65533
										}
									}
								}
							}
						}
					]
	
- docker inspect nervous_carver
	 - see **"Networks": {}** ==>> Means no network in container

					[
						{
							
								"Networks": {}
							
						}
					]
	
	
	
- docker network rm my-network

					my-network
	
- docker network ls


					NETWORK ID     NAME      DRIVER    SCOPE
					e08c374b6b36   bridge    bridge    local
					56586189be5a   host      host      local
					e4c236fa59cf   none      null      local
# docker network disconnect
- Disconnects a container from a network. The container must be **running** to disconnect it from the network.

# docker network subnet

- docker network create --subnet 192.168.0.0/16 my-subnet
	
			- 24a615e9d4fef17fcad6ac747ee2e33c9fb981e14fe0265791e55c8abdd04b2f
  
	- create docker network with **subnet option**
    - /16 CIDR means the first 16 bits are the network prefix, the remaining 16 bits are the host part.
	- Netmask (binary) = 11111111.11111111.00000000.00000000 → decimal 255.255.0.0.
	- **Network address** = keep the network bits, zero out the host bits → **192.168.0.0.**
	- **Broadcast address** = keep the network bits, set all host bits to 1 → **192.168.255.255.**
	- **First host** ( gateway ) = network address + 1 → **192.168.0.1.**
   	- **Second host** ( first container) = network address + 1 → **192.168.0.2.**
	- **Last host** ( last container) = broadcast address – 1 → **192.168.255.254.**

- docker inspect 24a615e9d4fef17fcad6ac747ee2e33c9fb981e14fe0265791e55c8abdd04b2f
	- 24a615e9d4fef17fcad6ac747ee2e33c9fb981e14fe0265791e55c8abdd04b2f = network id
		
				[
					{
						"Name": "my-subnet",
						"Id": "24a615e9d4fef17fcad6ac747ee2e33c9fb981e14fe0265791e55c8abdd04b2f",
						"Created": "2026-06-03T10:25:23.761206275Z",
						"Scope": "local",
						"Driver": "bridge",
						"EnableIPv4": true,
						"EnableIPv6": false,
						"IPAM": {
							"Driver": "default",
							"Options": {},
							"Config": [
								{
									"Subnet": "192.168.0.0/16",
									"Gateway": "192.168.0.1"
								}
							]
						},
						"Internal": false,
						"Attachable": false,
						"Ingress": false,
						"ConfigFrom": {
							"Network": ""
						},
						"ConfigOnly": false,
						"Options": {
							"com.docker.network.enable_ipv4": "true",
							"com.docker.network.enable_ipv6": "false"
						},
						"Labels": {},
						"Containers": {},
						"Status": {
							"IPAM": {
								"Subnets": {
									"192.168.0.0/16": {
										"IPsInUse": 3,
										"DynamicIPsAvailable": 65533
									}
								}
							}
						}
					}
				]

	- In the above response - 

   			"Gateway": "192.168.0.1" - Default route for containers.
			"Subnet": "192.168.0.0/16" - containers associated to this network will have IP addess from 192.168.0.2, 192.168.0.3 and so on..
			

- docker run -d --network my-subnet demo-app-service:latest
	- create first container with network. 			
			
				cfe15b9705afcebad06097e7f507c69dcdb488e4d4905fbe5af942dfbdd6eb51


- docker run -d --network my-subnet redis:7-alpine
	- create second container with network.			
			
				ca6205bebf98439844f694866898962eac6a4a80bb8d25afcd2237ed5e73ddf9


- docker inspect 24a615e9d4fe
	- now inspect network. it will show all the container associated to this network.
 	- The IP address of these containers will be decided by the subnet of the network.
  	- It's range 192.168.0.2 to 192.168.255.255		
				
				[
					{
						"Name": "my-subnet",
						"Id": "24a615e9d4fef17fcad6ac747ee2e33c9fb981e14fe0265791e55c8abdd04b2f",
						"Created": "2026-06-03T10:25:23.761206275Z",
						"Scope": "local",
						"Driver": "bridge",
						"EnableIPv4": true,
						"EnableIPv6": false,
						"IPAM": {
							"Driver": "default",
							"Options": {},
							"Config": [
								{
									"Subnet": "192.168.0.0/16",
									"Gateway": "192.168.0.1"
								}
							]
						},
						"Internal": false,
						"Attachable": false,
						"Ingress": false,
						"ConfigFrom": {
							"Network": ""
						},
						"ConfigOnly": false,
						"Options": {
							"com.docker.network.enable_ipv4": "true",
							"com.docker.network.enable_ipv6": "false"
						},
						"Labels": {},
						"Containers": {
							"ca6205bebf98439844f694866898962eac6a4a80bb8d25afcd2237ed5e73ddf9": {
								"Name": "distracted_shtern",
								"EndpointID": "d40b0825c9ce2b72daaa04cfcc76508ca6bab9323a11668679ed2cec4315ea5d",
								"MacAddress": "8e:2b:9d:d7:ff:7d",
								"IPv4Address": "192.168.0.3/16",
								"IPv6Address": ""
							},
							"cfe15b9705afcebad06097e7f507c69dcdb488e4d4905fbe5af942dfbdd6eb51": {
								"Name": "upbeat_robinson",
								"EndpointID": "5400b480a0eb6603b9de263fda6853fd481a8c9a8c9ca3288d303f0ed8fa9ada",
								"MacAddress": "86:3d:02:f2:02:42",
								"IPv4Address": "192.168.0.2/16",
								"IPv6Address": ""
							}
						},
						"Status": {
							"IPAM": {
								"Subnets": {
									"192.168.0.0/16": {
										"IPsInUse": 5,
										"DynamicIPsAvailable": 65531
									}
								}
							}
						}
					}
				]


# DNS 
- Only when a container is attached to a user‑defined bridge (or an overlay network).
- The default bridge (docker0) never gets an embedded DNS; containers on that network rely on the host’s /etc/resolv.conf.
- If you need containers to talk to each other by name:

		- docker network create mynet
		- docker run -d --name web  --network mynet nginx
		- docker run -d --name api  --network mynet nginx
  
	- inside any of them: ping web   (or ping web.mynet)

# 1️⃣ default bridge (what you already have)
	- docker run -d --name web nginx      # <-- uses default bridge
	- docker exec web cat /etc/resolv.conf
		- shows the host DNS (e.g., 192.168.65.7)
	- Because you started the container on the default bridge (docker0). In that mode Docker does not start the embedded DNS, so the file you see is the host‑derived resolv.conf (nameserver 192.168.65.7). If you create a custom network, the address changes to 127.0.0.11.

# 2️⃣ user‑defined bridge (embedded DNS)
	- docker network create mynet
	- docker run -d --name api --network mynet nginx
	- docker exec api cat /etc/resolv.conf
		- nameserver 127.0.0.11
# /etc/hosts inside the container
		- 127.0.0.1 localhost – the normal loop‑back entry (the container’s own “self”).
		- 172.17.0.2 124afd422cce – the IP address that Docker gave the container on the default bridge network followed by the container’s short‑ID. It is not the human‑readable name you gave with --name.
# /etc/resolv.conf inside the container
		- nameserver 192.168.65.7 – Docker simply copied the DNS server(s) that the host is using (or that the host’s DHCP gave it). The container will send all DNS queries to that address, not to Docker’s internal DNS.
		- nameserver 127.0.0.11 – When you attach a container to a user‑defined bridge network (or to an overlay network in Swarm/K8s), Docker starts a tiny DNS server inside the Docker daemon and binds it into every such container’s network namespace at the address 127.0.0.11
		

# Network Types 
- **default bridge driver ( network type )**
  	- When you launch a new container with docker run it automatically connects to this bridge network. 
    - default network
        - IP 172.17.0.1 aasigned to interface "docker0"
        - IP 172.17.0.2 aasigned to first container
        - IP 172.17.0.3 assigned to second container
        - and so on...
        - till 172.17.255.255
    - docker run -d redis
    	- The **"default bridge"** network (isolated).
  	- docker run -d -p 8080:80 redis
    	- The **"default bridge"** network (isolated)
    - docker run -d --network bridge redis
    	- The **"custom bridge"** network (isolated).
    - to access these containers from outside, we need port binding.
        - exposing containers to the world using port binding.
        - docker run --rm -d -P 80:80 redis 
    - Container can be accessed in broswer only if port binding done.
        - http://IP_ADDRESS_OF_HOST_MACHINE:80
    - containers communicate with each other using their internal IP address.
        - CONTAINER_1 - docker run --it -d --name redis-container redis
        - CONTAINER_2 - docker run --it -d --name nginx-container nginx
        - inside CONTAINER_1 (redis-container) IP 172.17.0.2
            - ping 172.17.0.3
            - ping google.com
            - "ip route" command
                - it will show "default via 172.17.0.1" which means routing via **interface docker0 ( 172.17.0.1 )**
                - The default gateway for the container is 172.17.0.1 on interface eth0.
                - All traffic that does not belong to the 172.17.0.0/16 network will be sent to the **Docker bridge (docker0) at 172.17.0.1**, which will then NAT it out to the host’s network (or another Docker network).
                - 
       - inside CONTAINER_2 (nginx-container) IP 172.17.0.3
            - ping 172.17.0.2 
            - ping google.com
        - CHALLENGE
            - our application(container) want to connect to database (container).
            - **after container restart, new IP address will be assiged, so communication using IPs is not correct.**
        - SOLUTION
          - "user-defined" Bridge
              - **Name registration** – The daemon registers the name web (and any --network-alias you supplied) with the embedded DNS, associating it with 172.18.0.2.
              - Every container on a user‑defined bridge gets a private /etc/resolv.conf that points to the IP 127.0.0.11 – Docker’s embedded DNS server (a tiny dnsmasq instance running inside the Docker daemon).
 			  - The daemon registers each container’s name (and any network aliases) with that embedded DNS.
			  - When a container asks the resolver library to resolve my‑service, the query is sent to 127.0.0.11. The embedded DNS replies with the container’s current IP address on that network.
              - "user-defined" network is isolated from all other networks ( default, none & host). can't talk to them.
              - **docker network create --driver bridge --subnet 182.8.x.x/16 custom-isolated-network**
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
- docker volume create **my-volume**
	- my-volume
	
- docker volume ls
	- DRIVER    VOLUME NAME
	- local     **my-volume**
	
- docker run -d -p 8080:8080 -v **my-volume**:/**folder-inside-container** my-app:1.1
	- c04f2e37c24dbc701ce87b55dca941bb51957838d6c573ba9689883874384f80
	
- docker ps
	- CONTAINER ID   IMAGE        COMMAND               CREATED          STATUS          PORTS                                         NAMES
	- c04f2e37c24d   my-app:1.1   "java -jar app.jar"   13 seconds ago   Up 13 seconds   0.0.0.0:8080->8080/tcp, [::]:8080->8080/tcp   confident_carson
	
- docker debug c04f2e37c24d
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

- docker run -d -p 8081:8080 -v **my-volume**:/**another-folder** my-app:1.1
	- 3c1809c99bb83b8dad993c57dffc6a37c1a54ec39e56ef78e22afb8201389ea2
	
- docker ps
	- CONTAINER ID   IMAGE        COMMAND               CREATED          STATUS          PORTS                                         NAMES
	- 3c1809c99bb8   my-app:1.1   "java -jar app.jar"   9 seconds ago    Up 8 seconds    0.0.0.0:8081->8080/tcp, [::]:8081->8080/tcp   recursing_yalow
	- c04f2e37c24d   my-app:1.1   "java -jar app.jar"   11 minutes ago   Up 11 minutes   0.0.0.0:8080->8080/tcp, [::]:8080->8080/tcp   confident_carson
	
- docker debug 3c1809c99bb8
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
