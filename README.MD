## Create user in docker group and check permissions

Run docker container -d (detached mode - demon mode) --rm(remove container after stop or kill - usefull for development) --name (name of container, by default will be hacker or scientist name-surname)
```
docker run -d --rm --name ContainerName ubuntu:20.04 -s /bin/bash username
```

## Docker logs
Tail last logs
```
docker logs (image name or name or container ID(* you can type first symbol of container id) )
```
LIVE logs add key -f (follow)
```
docker logs -f (image name or name or container ID(* you can type first symbol of container id) )
```

## Create user in docker group and check permissions

Create docker user (-m create homecategory)
```
useradd -m -s /bin/bash username
```

Add user to docker group (in example docker) <- user (username)
```
usermod -aG docker username
```

Check which groups are exist created user -> Print out applyed groups
```
id username
```

Check if user can run docker

```
su - username
```
```
docker --version
```


## Service Docker Main commands

Check if docker is running on Ubuntu
```
service docker status
```

Show all container
```
docker ps -a
```
Remove docker container by name (Copy full name, autogenerated if not setted container name), by image namem or container ID (You can type few start symbols, as example from 7ab0a37f41a5 you can type `docker rm 7ab`)
```
docker rm (image name or name or container ID(* you can type first symbol of container id) )
```


## Docker enviroment variables
1) Go inside container (container name) in -it(interactive mode) and run bash
```
docker exec -it (image name or name or container ID(* you can type first symbol of container id) ) /bin/bash
```
2) Inside container enviroment variables
```
env
```


## Docker inspect how build container
```
docker inspect (image name or name or container ID(* you can type first symbol of container id) )
```


## Docker resourse statistics
```
docker stats (image name or name or container ID(* you can type first symbol of container id) )
```


## Remove all images and STOPPED container
Main idea
1) Stop container `docker stop (image name or name or container ID(* you can type first symbol of container id) )`
2) Remove container `docker rm (image name or name or container ID(* you can type first symbol of container id) )`
3) Remove Image ` docker rmi (image name or name or container ID(* you can type first symbol of container id) )`

To remove all stopped containers and images -a(remove images) --volumes(remove persistent data - volumes)
```
docker system prune -a --volumes (image name or name or container ID(* you can type first symbol of container id) )
```


## Docker port forwarding mapping inside docker to "world"
Check open connection on server
```
netstat -tulpen
```

Check ethernet interfaces and IP
```
ip a
```

## Docker network
# network types
1) macvlan - IP and MAC will be different
2) ipvlan - IP will be different but MAC the same
3) none - no network (not possible to connect form world or inside)
4) host - IP the same as server
5) bridge - connect from "qorld" if use port forwarding 80 `-p 80:80`
```
docker network create -d bridge --subnet 192.168.10.0/24 --gateway 192.168.10.1 myNetworkName
```
Create MACVLAN network with IP 192.168.100.99
```
docker network create -d macvlan (-d driver) --subnet 192.168.100.0/24 --gateway 192.168.100.1 --ip-range 192.168.100.99/32 -o parent=ens18 (ens18 - network inteface) MACNetworkName
```


Check available networks
```
docker network ls
```

Inspect - networks details
```
docker network inspect (network name myNetworkName)
```

Connect container to network
```
docker network connect (network name myNetworkName) (container name or id)
```

Disconnect container to network
```
docker network disconnect (networkID - can get NetworkID `docker inspect (container name)`) (container name or id)
```

## Docker images
1) Create dockerfile `touch dockerfile`
2) Edit with vim `vi dockerfile` and add some instructions `FROM ubuntu:22.04 CMD ["echo", "Echo message"]`
3) Build image `docker build .`
4) Check unnamed docker-image `docker images`
5) Update - revise tag and version `docker tag (image name or ID) imagename:v1`

To build with tag add `-t` to build with image repository name and image tag
```
docker build -t imagename:v1
```
