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

docker container ls -a
docker container rm <ID[,ID][,ID]...>
docker container ls -a
docker container rm -f <ID>
docker container ls -a

