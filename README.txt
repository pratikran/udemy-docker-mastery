DOCKER INSTALL

Installing on Windows 10 (Pro or Enterprise)
  https://www.docker.com/docker-windows
Installing on Windows 7, 8, or 10 Home Edition
  https://www.docker.com/products/docker-toolbox
    http://192.168.99.100
Installing on Mac
    https://www.docker.com/docker-mac
  OLDER MAC < OSX Yosemite 10.10.3
    https://www.docker.com/products/docker-toolbox
Installing on Linux
  apt/yum install docker.io
    
  add their repository and install all dependencies: 
    curl -sSL https://get.docker.com/ | sh
  manual method by following specific instructions on the Docker Store for your distribution
    https://store.docker.com/editions/community/docker-ce-server-ubuntu
  
IF NOTHING WORKS
  http://play-with-docker.com/
    run one or more Docker instances inside your browser, and give you a terminal to use it with
    
get.docker.com
https://github.com/docker/compose/releases
https://github.com/docker/machine/releases

SHELL AND TAB COMPLETION 
  WINDOWS SHELL/TERM
    http://cmder.net/
    https://conemu.github.io/
  WINDOWS POWERSHELL TAB COMPLETION
    https://docs.docker.com/docker-for-windows/#set-up-tab-completion-in-powershell
  MAC SHELL/TERM
    https://www.iterm2.com/
  MAC TAB COMPLETION
    http://blog.alexellis.io/docker-mac-bash-completion/
  MAC
    http://www.bretfisher.com/shell

Docker Version Format Change in Early 2017
  https://blog.docker.com/2017/03/docker-enterprise-edition/
  
docker-machine env default
    @FOR /f "tokens=*" %i IN ('docker-machine env default') DO @%i
    OR
    eval $("C:\Program Files\Docker Toolbox\docker-machine.exe" env default)

docker-machine ls
docker-machine start
docker-machine stop
docker-machine ip

docker version
docker info

docker <command> <sub-command> <options>

docker container run --publish 80:80 nginx
docker container run --publish 80:80 --detach nginx

docker container ls
docker container stop <ID>
docker container ls
docker container ls -a
docker container run --publish 80:80 --detach --name webhost nginx
docker container logs webhost
docker container top webhost

docker container --help
docs.docker.com

docker container ls -a
docker container rm <ID[,ID][,ID]...>
docker container ls -a
docker container rm -f <ID>
docker container ls -a

docker run --name mongo -d mongo
docker top mongo
docker stop mongo
docker ps
ps aux | grep mongod
docker top mongo
  error
ps aux | grep mongod
docker start mongo
docker top mongo
ps aux | grep mongod


WINDOWS DOCKER CONTAINERS: DOCKER IS NOT JUST LINUX
  Windows Containers and Docker 101
    https://www.youtube.com/watch?v=066-9yw8-7c
  Windows and Linux Parity with Docker
    https://www.youtube.com/watch?v=4ZY_4OeyJsw
  Docker + Microsoft - Investing in the Future of your Applications
    https://www.youtube.com/watch?v=QASAqcuuzgI
    
docker container run --publish 3306:3306 --detach --name db --env MYSQL_RANDOM_ROOT_PASSWORD=yes mysql
    (docker container run -p 3306:3306 -d --name db -e MYSQL_RANDOM_ROOT_PASSWORD=yes mysql)
docker container logs mysql

docker container run --publish 8080:80 --detach --name webserver httpd
    (docker container run -p 8080:80 -d --name webserver httpd)
docker container run --publish 80:80 --detach --name proxy nginx
    (docker container run -p 80:80 -d --name proxy nginx)

docker container ls -a
docker ps -a

docker container stop <ID/name>,<ID/name>...
docker container rm <ID/name>,<ID/name>...

docker container ls -a
docker ps -a

docker container run -d --name proxy nginx
docker container run -d --name mysql -e MYSQL_RANDOM_ROOT_PASSWORD=yes mysql

docker container top db
docker container top proxy

docker top db
docker top proxy

docker container inspect db
docker container stats --help
docker container stats
docker container stats db
docker container stats proxy
docker container ls -a

docker container run --name ubuntu ubuntu

docker container run --help
docker container run -it --name proxy-it nginx bash
    $# exit
docker container start -ai proxy-it

docker container exec -it db bash

docker pull alpine
docker image
docker container run -it alpine bash
    ERROR: bash: executable file not find in $PATH
docker container run -it alpine sh
    $# apk add bash

PACKAGE MANAGEMENT
  https://www.digitalocean.com/community/tutorials/package-management-basics-apt-yum-dnf-pkg
  
DOCKER NETWORKS: CONCEPTS  
Docker Networks: Concepts for Private and Public Comms in Containers
  
  Docker's --format option for filtering cli output
      https://docs.docker.com/engine/admin/formatting/
      
      
docker container run -p 80:80 --name webhost -d nginx
docker container port webhost
  172.17.0.2

docker container inspect --format '{{ .NetworkSettings.IPAddress }}' webhost

FIXME: Change In Official Nginx Image Removes Ping
  
  A recent June 2017 change in the official nginx image removes ping
      https://hub.docker.com/_/nginx (nginx  or nginx:latest) 
  
  Inplace of
  docker container run <stuff> nginx
  Do this
  docker container run <stuff> nginx:alpine
  
  There are other ways to solve this, including adding the ping util with apt-get, making your own image, etc.
    https://www.udemy.com/docker-mastery/learn/v4/questions/2487292
  
DOCKER NETWORKS
Docker Networks: CLI Management of Virtual Networks

docker network ls
  bridge, host, none
docker network inspect bridge
docker network create my_net_app
docker network create --help

docker container run --name new_nginx --network my_net_app -d nginx:alpine
docker network inspect my_net_app

docker network --help
docker ps -a
docker network ls -a

docker network connect 411d5fc6ed90 ca30b4195cc7
docker container inspect webhost
  172.17.0.2
  172.18.0.3
docker network disconnect 411d5fc6ed90 ca30b4195cc7  
  
Docker Networks: DNS and How Containers Find Each Other
  
  DNS NAMING
docker network inspect my_net_app
docker container run --name my_nginx --network my_net_app -d nginx:alpine
docker container exec -it my_nginx ping new_nginx
docker container exec -it new_nginx ping my_nginx

docker network ls
docker container create --help
  --link option 

CURL ASSIGNMENT
docker container run --rm -it centos:7 bash
  yum update curl
  exit
docker container run --rm -it ubuntu:14.04 bash
  apt-get update && at-get install -y curl
  exit
docker ps -a


ASSIGNMENT: DNS Round Robin Test

docker pull elasticsearch:2
docker network create dude
docker container run -d --net dude --net-alias search elasticsearch:2
docker container run -d --net dude --net-alias search elasticsearch:2
docker container ls
docker container run --rm --net dude alpine nslookup search
docker container run --rm --net dude centos curl -s search:9200 


hub.docker.com
docker pull nginx
docker pull nginx:1.11.9
Official Docker Image Specification
  https://github.com/moby/moby/blob/master/image/spec/v1.md
List of Official Docker Images
  https://github.com/docker-library/official-images/tree/master/library
Images and Containers From Docker Docs
   https://docs.docker.com/engine/userguide/storagedriver/imagesandcontainers/
   
DOCKER IMAGES
  union filesystem
  
docker images
docker image ls
docker history nginx:latest
docker history mysql

docker image layers 
  local cache
   upload/download only image layers not in cache
   same layers are stored only once across all images
   each layer has a sha hash
  containers
    copy on write
 
docker image inspect nginx
  show metadata 

DOCKER IMAGE TAGGING AND PUSH TO DOCKER HUB

docker image tag --help
docker image ls
docker pull mysql/mysql-server
docker pull bretfisher/nodemongoapp
docker pull nginx:mainline
docker image tag nginx bretfisher/nginx
docker image tag nginx pratikran/nginx
docker image push pratikran/nginx

login/logout to hub.docker.com

docker login
docker logout

docker image push pratikran/nginx
docker image tag pratikran/nginx pratikran/nginx:testing
docker image push pratikran/nginx
docker image ls

BUILDING IMAGES
DOCKERFILE BASICS
  FROM
  ENV
  RUN
  EXPOSE
  CMD



