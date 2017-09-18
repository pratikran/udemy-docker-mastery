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

git clone https://github.com/pratikran/udemy-docker-mastery
cd udemy-docker-mastery
cd dockerfile-sample-1
docker image build -t custom_nginx .
  on hub.docker.com
    docker image build -t pratikran/custom_nginx .
docker image ls
EDIT Dockerfile 
  EXPOSE 80 443 8080
docker image build -t custom_nginx .
docker image ls

EXTENDING OFFICIAL IMAGES

cd ../dockerfile-sample-2
docker container run -p 80:80 --rm nginx

DOCKERFILE

  FROM
  WORKDIR
  COPY
  
docker image build -t nginx-with-html .
docker container run -p 80:80 --rm nginx-with-html

docker image ls
docker image tag nginx-with-html:latest pratikran/nginx-with-html:latest
docker image ls

ASSIGNMENT: BUILD YOUR OWN IMAGE

cd ../dockerfile-assignment-1
vim Dockerfile
docker build -t testnode .
docker image ls
docker container run --rm -p 80:3000 testnode 
docker tag testnode pratikran/testing-node
docker push pratikran/testing-node
docker rmi testnode
docker container run --rm -p 80:3000 pratikran/testing-node


DOCKER CONTAINER LIFETIME AND PERSISTENT DATA

  An introduction to immutable infrastructure
    https://www.oreilly.com/ideas/an-introduction-to-immutable-infrastructure
    
  The twelve-factor app
    https://12factor.net/
  
  12 Fractured Apps
    12 Factor on Containers
      https://medium.com/@kelseyhightower/12-fractured-apps-1080c73d481c
      
  
  VOLUMES
  BIND MOUNTS
  
  Dockerfile
  
  hub.docker.com
    mysql
      Dockerfile
    
VOLUMES
  created at container runtime, in Dockerfile, in cmdline beforehand

docker pull mysql
docker image inspect mysql

docker container run -d --name mysql -e MYSQL_ALLOW_AMPTY_PASSWORD=True mysql
docker ps -a
docker container inspect mysql
  mounts
docker volume ls
docker container run -d --name mysql2 -e MYSQL_ALLOW_AMPTY_PASSWORD=True mysql

docker container stop mysql mysql2
docker container ls
docker container ls -a
docker container rm mysql mysql2
docker volume ls

docker container run -d --name mysql -e MYSQL_ALLOW_AMPTY_PASSWORD=True -v /var/lib/mysql mysql
docker container run -d --name mysql -e MYSQL_ALLOW_AMPTY_PASSWORD=True -v mysql-db:/var/lib/mysql mysql

docker volume ls
docker container inspect mysql

docker voulme create --help

BIND MOUNTS
  created at container runtime only
  
cd ../dockerfile-sample-2
cat Dockerfile

docker container run -d --name nginx -p 80:80 -v $(pwd):/usr/share/nginx/html nginx
  http://192.168.99.100
  edit index.html
  http://192.168.99.100
docker container run -d --name nginx2 -p 8080:80 nginx
  http://192.168.99.100


ASSIGNMENT: Database Upgrades with Named Volumes

hub.docker.com
  postgres
    tags
      9.6.1
        VOLUMES

docker container run -d --name psql -v psql:/var/lib/postgresql/data postgres:9.6.1
docker container logs -f psql 
docker container stop psql
docker container run -d --name psql2 -v psql:/var/lib/postgresql/data postgres:9.6.2
docker container logs -f psql2


ASSIGNMENT: Edit Code Running in Containers with BIND MOUNTS

Jekyll, a Static Site Generator (just as background info, no need to install)
    https://jekyllrb.com/

docker run -p 80:4000 -v $(pwd):/site bretfisher/jekyll-serve
  (some ERRORs, try later)
  

DOCKER COMPOSE
  initially called fig
docker-compose.yml

YAML
  http://www.yaml.org/start.html
  http://www.yaml.org/refcard.html
COMPOSE
  https://docs.docker.com/compose/compose-file/compose-versioning/
  https://github.com/docker/compose/releases

CLI
  docker-compose
  Not for production grade 
  Good for local dev and test

Basic Compose Commands
  Download via Github for Linux
    https://github.com/docker/compose/releases
  
docker-compose up
docker-compose down

docker-compose -f <yaml filename> up

docker-compose up -d
  background run

cd ../compose-sample-2

docker-compose up
  logs are dumped on STDOUT by default
  
  ERROR:
    Windows 10 Home 64bit, Docker ToolBox, docker version 17.07.0-ce, docker-compose 1.15.0
  
"""""""""""""""""""""""""""""""""""""""""""""""""""""
ERROR: for proxy  Cannot start service proxy: oci runtime error: container_linux.go:262: starting container process caused "process_linux.go:339: container init caused \"rootfs_linux.go:57: mounting \\\"/f/Code/devops/udemy-bretfisher/udemy-docker-mastery/compose-sample-2/nginx.conf\\\" to rootfs \\\"/mnt/sda1/var/lib/docker/aufs/mnt/6968110f68ebe6c67a726549f6b76286821b1e4a6825c5a318ccfd7048d006e9\\\" at \\\"/mnt/sda1/var/lib/docker/aufs/mnt/6968110f68ebe6c67a726549f6b76286821b1e4a6825c5a318ccfd7048d006e9/etc/nginx/conf.d/default.conf\\\" caused \\\"not a directory\\\"\""
    : Are you trying to mount a directory onto a file (or vice-versa)? Check if the specified host path exists and is the expected  type
"""""""""""""""""""""""""""""""""""""""""""""""""""""

SOLUTION:
"""""""""""""""""""""""""""""""""""""""""""""""""""""
https://github.com/moby/moby/issues/23992
https://github.com/docker/compose/issues/2268

Shared the new drive in VirtualBox, 
docker-compose.yml
  - volumes map done for folders instead of files, ie nginx.conf map to default.conf was removed, folder to folder map kept, source nginx.conf was duplicated as default.conf to match file expected in container ie default.conf
"""""""""""""""""""""""""""""""""""""""""""""""""""""

docker-compose logs
docker-compose ps
docker-compose top
docker-compose down

ASSIGNMENT: DOCKER-COMPOSE YAML for Multi-Container Service

cd ../compose-assignment-2
docker pull drupal
docker image inspect drupal
    ContainerConfig
            ExposedPorts
                80/tcp
vim docker-compose.yml

docker-compose up
ERROR: Named volume "drupal-modules:/var/www/html/modules:rw" is used in service "drupal" but no declaration was found in the volumes section.

SOLUTION: Add separate volumes section with named volumes names copied from drupal service volumes 

hub.docker.com
  read postgres documentation how db works
  similarly for other services
  
http://192.168.99.100:8080
  follow drupal install instruction
  
docker-compose down -v
  to remove volumes use -v


ADDING IMAGE BUILDING TO COMPOSE FILES

cd ../compose-sample-3
cat docker-compose.yml

  if image tag is not used docker-compose will create a unique name based on directory and servicename

docker-compose up
  WARNING: Image for service proxy was built because it did not already exist. To rebuild this image you must use `docker-compose build` or `docker-compose up --build`
  
http://192.168.99.100/
  
Bind Mount
  edit 
    index.html
  http://192.168.99.100/
  
docker-compose down --rmi local

ASSIGNMENT: COMPOSE BUILD AND RUN 
  drupal image build and run

cd ../compose-assignment-2
  EDIT
    Dockerfile
    docker-compose.yml
docker-compose up
  configure drupal
    http://192.168.99.100:8080
  
docker-compose down
  volumes preserved
docker-compose up
  data used from persistent volumes
  

SWARM MODE: BUILT IN ORCHESTRATION
  Clustering Solution built in with docker
  swarm classic in version <1.12 was different.
  Added in 1.12 (summer 2016) via swarmkit toolkit.
  Not enabled by default, needs to be enabled.
  
  
docker swarm deep dive 
  https://www.youtube.com/watch?v=dooPhkXT9yI
  https://www.youtube.com/watch?v=_F6PSP-qhdA
  
Heart of Swarmkit: Topology Management
  https://speakerdeck.com/aluzzardi/heart-of-the-swarmkit-topology-management
  https://www.youtube.com/watch?v=EmePhjGnCXY
  
Raft consensus visualization(swarm db, how it stays in sync across nodes)
  http://thesecretlivesofdata.com/raft/
  
CREATE FIRST SERVICE , SCALE LOCALLY
  deploy services to a swarm
    https://docs.docker.com/engine/swarm/services/
    
check swarm enabled
docker info

initialize
docker swarm init
      """"""""""""""""""""""
      Error response from daemon: could not choose an IP address to advertise since this system has multiple addresses on different interfaces (10.0.2.15 on eth0 and 192.168.99.100 on eth1) - specify one with --advertise-addr
      """"""""""""""""""""""

docker-machine ip      
docker swarm init --advertise-addr 192.168.99.100

      """"""""""""""""""""""
      Swarm initialized: current node (3actciwj7uezg107q2af829it) is now a manager.

      To add a worker to this swarm, run the following command:

      docker swarm join --token SWMTKN-1-3li4vru26e5v6wzhzyjz9a1l8z58bs3dnkdejwpcl9hj7kl1h3-0cybt1a7o5nj7vb97sqehzbo0 192.168.99.100:2377

      To add a manager to this swarm, run 'docker swarm join-token manager' and follow the instructions.
      """"""""""""""""""""""

docker swarm init
docker-machine ip 
docker swarm init --advertise-addr 192.168.99.100

SINGLE NODE SWARM
docker node ls
    there is only one leader
docker node --help
docker swarm --help
docker service --help
docker service create alpine ping 8.8.8.8
docker service ls
docker service ps <NAME{eg:nifty_goldberg here from above}>
docker container ls
docker service update <SERVICE{eg:k2hmzypcebg8 here from docker service ls}> --replicas 3
docker service ls
docker service ps <NAME{eg:nifty_goldberg here from above}>
docker update --help
  for container runtime to update configurations
    this may require restart
docker service update --help
    this will be done without any restart for the swarm or automatic retarts within, very transparently
docker container ls
docker service ls
docker service ps nifty_goldberg
docker service rm nifty_goldberg
docker service ls
docker container ls
docker container ls

SWARM MULTI-NODE

  CREATE 3-NODE SWARM CLUSTER
  
  Digital Ocean Coupon for $10
        https://www.digitalocean.com/?refcode=b813dfcad8d4&utm_campaign=Referral_Invite&utm_medium=Referral_Program&utm_source=CopyPaste
  Create and Upload a SSH Key to Digital Ocean
        https://www.digitalocean.com/community/tutorials/how-to-use-ssh-keys-with-digitalocean-droplets
  Docker Swarm Firewall Ports
        http://www.bretfisher.com/docker-swarm-firewall-ports/
  Configure SSH for Saving Options for Specific Connections
        https://www.digitalocean.com/community/tutorials/how-to-configure-custom-connection-options-for-your-ssh-client
  
  
  OPTIONS
    IN BROWSER
      play-with-docker.com
    DOCKER-MACHINE + VITUALBOX
      free, local run, needs machine with 8Gb RAM
    DIGITAL OCEAN+DOCKER INSTALL
      per month charge, can use referral code to get $10 free
    ROLL YOUR OWN
      docker-machine
        on local, AWS< GCC, DO, AZURE
         meant for dev/test not production
      get.docker.com
        install docker anywhere
    
play-with-docker.com
  (docker within docker container)
  node 1
    docker info
    ping node2
  node 2
  node 3
  
docker-machine+VIrtualBox
  >0.10.0
  
  docker-machine create node1
  docker-machine env node1
  docker info
    Name
    
Digital Ocean
  
docker-machine
  docker-machine create node1
  docker-machine create node2
  
  on default node
docker swarm init --advertise-addr 192.168.99.100
docker swarm join-token manager
  
  on node1
  docker swarm join --token SWMTKN-1-3li4vru26e5v6wzhzyjz9a1l8z58bs3dnkdejwpcl9hj7kl1h3-0cybt1a7o5nj7vb97sqehzbo0 192.168.99.100:2377

on default
docker node ls
docker node update --role manager node1
docker swarm join-token manager

on node2
docker swarm join --token SWMTKN-1-3li4vru26e5v6wzhzyjz9a1l8z58bs3dnkdejwpcl9hj7kl1h3-2t36ajyn5my12pdctnvgvfk1d 192.168.99.100:2377

on default
docker node ls
docker service create --replicas 3 alpine ping 8.8.8.8
docker service ls
docker node ps
docker service ps gracious_mclean
docker service rm gracious_mclean


SWARM: SCALING OUT WITH OVERLAY NETWORKING
  --drive overlay
  container-to-container networking in single swarm
  IPSec(AES) encryption
  each service with multiple networks
  
  docker network create --driver overlay my_drupal
  docker network ls
  docker service create --name psql --network my_drupal  -e POSTGRES_PASSWORD=password postgres
  docker service ls
  docker service ps psql
  
  docker container logs psql.1....
  docker service create --name drupal --network my_drupal -p 8080:80 drupal
  docker service ls
  watch docker service ls
  docker service ps drupal
      http://IP_DEFAULT:8080
      http://IP_NODE1:8080
      http://IP_NODE2:8080
  on all node
    docker ps -a


SCALING OUT WIHT ROUTING MESH
  use swarm mode routing mesh
      https://docs.docker.com/engine/swarm/ingress/
      
  uses IPVS in Linux kernel 
  
  Load Balancing across Tasks
    container-to-container (overlay network)
    published ports open on all nodes
      external traffic incoming to all node is listened to
    each node has a load balancer
      routing to local and external nodes
    stateless load balancing
    L3(tcp) LB, not L4(DNS) LB
      Nginx or HAProxy or AWS ELB etc
      Docker EE - built in L4 LB
      some useful links
          http://collabnix.com/docker-17-06-swarm-mode-now-with-macvlan-support/

docker service create --name search --replicas 3 -p 9200:9200 elasticsearch:2
docker service ps search
curl localhost:9200
  
  
ASSIGNMENT: SWARM CREATE MULTI-SERVICE APP
  cd ../swarm-app-1
  
docker network create --driver overlay backend
docker network create --driver overlay frontend

vote
docker service create --name vote -p 80:80 --replicas 2 --network frontend dockersamples/examplevotingapp_vote:before
docker service create --name redis --replicas 2 --network frontend redis:3.2
docker service create --name worker --network frontend --network backend dockersamples/examplevotingapp_worker
docker service create --name db --network backend --mount type=volume,source=db-data,target=/var/lib/postgresql/data postgres:9.4
docker service create --name result -p 5001:80 --replicas 2 --network backend dockersamples/examplevotingapp_result:before

docker service ls
docker service ps redis
docker service ps result
docker service ps db
docker service ps worker
docker service ps vote

docker service logs result
    this is experimental but enabled by default in >= docker 17.05.0-ce
    
to enable experimental features, useful to know docker Configuration file
/etc/docker/daemon.json
  {"experimental":"true"}
  
for this do all nodes - default,node1,node2
  docker-machine ssh <node-name>
  sudo ls -la /etc/docker/daemon.json
  sudo sh -c 'echo {\"experimental\":\"true\"} >> /etc/docker/daemon.json'
  sudo cat /etc/docker/daemon.json

docker service logs result
docker service ps result

http://192.168.99.100
http://192.168.99.100:5001

docker service rm redis result db worker vote
docker service ps redis result db worker vote
docker service ls
docker ps -a



SWARM STACKS and PRODUCTION GRADE COMPOSE
  SWARM STACKS
    added docker >1.13
    COMPOSE files for SERVICES, NETWORKS, VOLUMES
    COMMAND
      docker stack deploy
      VS
      docker service create
    deploy:
    no build:
    docker-compose 
        ignores deploy:
    swarm 
        ignores build:
    docker-compose cli not needed on swarm 
    not everything needed to be in stacked file
    
STACK
  YAML
    SERVICES
    VOLUMES
    OVERLAY NETWORKS
    SECRETS
    
    is a COMPOSE file
      version >= 3
      
  cd ../swarm-stack-1
  cat example-voting-app-stack.yml
  
  docker stack deploy -c example-voting-app-stack.yml voteapp
  
  docker stack --help
  docker stack ls
  docker stack ps voteapp
  docker stack services voteapp
  docker container ls
  docker network ls
  
  result
    http://192.168.99.100:5001/
  visualizer
    http://192.168.99.100:8080/
  vote
    http://192.168.99.100:5000/
  
  vim example-voting-app-stack.yml
    vote:
      replicas: 5
  docker stack deploy -c example-voting-app-stack.yml voteapp
  
  result
    http://192.168.99.100:5001/
  visualizer
    http://192.168.99.100:8080/
  vote
    http://192.168.99.100:5000/
    
  docker stack ps voteapp
  docker stack services voteapp
  docker ps -a
  
  
SWARM; SECRETS STORAGE
    username/password
    TLS certs/SSH keys
    unshareables
    
    generic strings/binary content
     >1.13 RAFT DB is encrypted on disk on manager nodes 
    secrets - nit files but container in-memory fs, saved on swarm, assigned to services, then fetched by containers as needed
    /run/secrets/<secret_name|secret_alias>
    secrets are swarm specific and saved in its db
    but for local dev workaround, docker-compose can use file based secrets, not secure
    
    cd ../secrets-sample-1
    cat psql_user.txt
    
    SECRETS 
    file based
        docker secret create psql_user psql_user.txt
        echo "mypassword" | docker secret create psql_pass - 
        
        security concerns
          api called to remote using a file secret on local
          root user profile file 
          
      docker secret inspect psql_user
      docker service create --name psql --secret psql_user --secret psql_pass -e POSTGRES_PASSWORD_FILE=/run/secrets/psql_pass -e POSTGRES_USER_FILE=/run/secrets/psql_user postgres
      docker service ps psql
      docker ps -a
      docker exec -it psql.1.7agr1prwca29qces8k5unrl27 bash
        $# ls /run/secrets
        $# cat psql_user; cat psql_pass
        $# exit
        
      docker logs psql.1.7agr1prwca29qces8k5unrl27
      docker service ps psql
      docker service update --secret-rm
        on this command it will recreate the container
        
    
        secrets with swarm stacks
            stack version > 3.1

          cd ../secrets-sample-2
          docker-compose.yml
              secrets
                file: or 
                external:
              then assign to containers in services
          docker stack deploy -c docker-compose.yml mydb
          docker secret ls
          docker stack rm mydb
    
USING SECRETS WITH LOCAL DEV MACHINE
  
    cd ../secrets-sample-2
    docker node demote efault
    docker swarm leave
    docker node rm default
    docker info
      Swarm: inactive
    
    docker-compose up -d
        WINDOWS TOOLBOX
        """"""""""""""""""""""""""""""""""""""""
        ERROR: for secretssample2_psql_1  Cannot create container for service psql: invalid bind mount spec "F:\\Code\\devops\\udemy-bretfisher\\udemy-docker-mastery\\secrets-sample-2\\psql_user.txt:/run/secrets/psql_user:ro": invalid volume specification: 'F:\Code\devops\udemy-bretfisher\udemy-docker-mastery\secrets-sample-2\psql_user.txt:/run/secrets/psql_user:ro'
        """"""""""""""""""""""""""""""""""""""""
        debugging
            docker-compose --verbose config
            docker-compose version
            docker version
        docker-machine ssh default
              install docker-compose
              share f drive in virtualbox
              cd to_path/secrets-sample-2/
          docker-compose up -d
          docker-compose exec psql cat /run/secrets/psql_user
    docker-compose
        secrets:
          file:
            this is for development
          external:
            use in production


ASSIGNMENT: CREATE SWARM STACK WITH SECRETS AND DEPLOY
  
   cd ../compose-assignment-2
   
   docker-compose.yml
     swarm doesnt build
        so, build key can be removed
     POSTGRES_PASSWORD=password
        to
        POSTGRES_PASSWORD_FILE=/run/secrets/psql-pw
     add
        secrets sections
          make external 
   
   echo "password1" | docker secret create psql-pw -
   docker stack deploy -c docker-compose.yml drupal
        ERROR: secrets Additional property secrets is not allowed
        Windows 10 Home 64bit, Docker ToolBox, docker version 17.07.0-ce, docker-compose 1.15.0
        
        solution
          docker-compose file version
            changed to 3.1 from 3
   docker stack ps drupal
   
FULL LIFECYCLE WITH COMPOSE
    cd ../swarm-stack-3/
    
    Multiple docker compose file
        https://docs.docker.com/compose/extends/#multiple-compose-files
    Docker compose in production
        https://docs.docker.com/compose/production/
        
    LOCAL DEV
    docker-compose up -d
    docker inspect swarmstack3-drupal-1
        Mounts 
    CI
    docker-compose -f docker-compose.yml -f docker-compose.test.yml up -d
          base yaml first, then test yaml
    docker inspect swarmstack3-drupal-1
          bind Mount not listed
    PRODUCTION
    docker-compose -f docker-compose.yml -f docker-compose.test.yml config > output.yml
    
    
    docker-compose multiple file
        extends keyword
          removed in compose file >2.1
            but could be added in later versions
            


DOCKER IMAGE REGISTRY
  https://hub.docker.com/
  
  docker hub
  docker store
  docker cloud
  swarm connect to docker hub locally
  build own registry
  third party registries
  
  DOCKER HUB
      public registry
      registry + lightweight image building
      bitbucket/github link to hub and build images
      chaining image building
      
      
      image building link/webhook
          create > create automated build
  
  DOCKER STORE
      https://store.docker.com/
      released summer 2016
      Download docker software
      reliable software from 3rd parties
      like apple store
        patnered software and could be premium too
        
  DOCKER CLOUD
      CI/CD, Server Ops
      Web Based DOcker Swarm Creation and Management
      https://cloud.docker.com
      
      uses popular cloud hosts, also bring your own servers
      automated image building, testing, deployment
      advance than docker hub free jobs
      private image security scan
          on docker hub this is done on official images
      CVE - Common Vulnerability and exposure
          by Government of USA, HomeLand Security,
            done for all softwares
      See a quick how-to video on Swarms fleet management feature on YouTube.
            https://youtu.be/VJmbCioYKGg
      
      
DOCKER REGISTRY UNDERSTANDING
    Configuration
      https://docs.docker.com/registry/configuration/
    Garbage Collection
      https://docs.docker.com/registry/garbage-collection/
    Mirror of DOcker HUb
      https://docs.docker.com/registry/recipes/mirror/
      
    Private Registry
    Part of Docker DIstribution on Github repo
    Registry image on docker hub
    basic auth, web api, no ui
    api + storage
    support storage loca, S3, GC, alibaba, Openstack swift
    
RUN PRIVATE REGISTRY
    docker container run -d -p 5000:5000 --name registry registry
    docker container ls
    docker image ls
    TAGS
        docker Hub
            <image name>:<version>
        other registry
            add host as well
    docker pull hello-world
    docker run hello-world
    docker tag hello-world 127.0.0.1:5000/hello-world
    docker image ls
    docker push 127.0.0.1:5000/hello-world
         hostIP tag will make it push it to local registry
    docker image remove hello-world
         removed local copy
    docker image remove 127.0.0.1:5000/hello-world
        remove referencing container first if it is running
    docker image ls
    docker pull 127.0.0.1:5000/hello-world
    docker image ls
    Recreate Registry with persistent volume
        docker container kill registry
        docker container rm registry
    docker container run -d -p 5000:5000 --name registry -v $(pwd)/registry_data:/var/lib/registry registry
    ls -la ./registry_data
    docker push 127.0.0.1:5000/hello-world
    ls -la ./registry_data
    tree registry-data/
    
ASSIGNMENT: Secure Docker Registry With TLS and Authentication    
    Find this section in the following File in this repositry
        Linked2ReadMeTXT.txt
    
    
SWARM with DOCKER REGISTRY
    No 'docker run' command
      but
        'docker service' command
    
    Setup test swarm
        play-with-docker.com
          click on 'rinch' icon 
            use templates
        docker node ls
        docker service create --name registry --publish 5000:5000 registry
        docker service ps registry
        
            clicking on port button
                in the new tab url
                    add /v2/_catalog
                      see catalog of registries as output in browser
        
        docker pull hello-world
        docker tag hello-world 127.0.0.1:5000/hello-world
        docker push 127.0.0.1:5000/hello-world
             
            check the catalog of registries at url at location /v2/_catalog
        
        docker pull nginx
        docker tag nginx 127.0.0.1:5000/nginx
        docker push nginx 127.0.0.1:5000/nginx
            check the catalog of registries at url at location /v2/_catalog
                {"registries":["hello-world","nginx"]}
        docker service create --name nginx -p 80:80 --replicas 5 --detach=false 127.0.0.1:5000/nginx
        
        Each Swarm node can pull image from some central registry, they cannot pull it from any other node itself.
            registry accessible by all node is a must
            
 
 THIRD PARTY IMAGE REGISTRIES
        Check the linked file in this repository
          Linked2ReadMeTXT.txt
          
 
        
        
        
        
    
    
      
      
    
    
        
   
