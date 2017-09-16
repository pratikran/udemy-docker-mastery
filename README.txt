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

docker container inspect --format '{{ .NetworkSettings.IPAddress }}' webhost



