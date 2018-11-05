(Also tested for docker toolbox on windows (if on windows skyp installation and jump directly to git clone))
# Install wordpress with docker on centos 7

## Set up repositories
```
sudo yum update

sudo yum remove docker \
                  docker-client \
                  docker-client-latest \
                  docker-common \
                  docker-latest \
                  docker-latest-logrotate \
                  docker-logrotate \
                  docker-selinux \
                  docker-engine-selinux \
                  docker-engine
                  
sudo yum install -y yum-utils \
  device-mapper-persistent-data \
  lvm2                  

sudo yum-config-manager \
    --add-repo \
    https://download.docker.com/linux/centos/docker-ce.repo  
```

## Install and enable docker,docker-compose
```
sudo yum install docker-ce

sudo systemctl start docker
sudo systemctl enable docker

sudo curl -L "https://github.com/docker/compose/releases/download/1.22.0/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose

sudo chmod +x /usr/local/bin/docker-compose
```
## Install git and clone wordpress repo
```
sudo yum install git

git clone https://gitlab.z-hosts.com/adrian.lux/docker-wordpress.git
```
## Set up and start wordpress

Edit username and passwd in docker-compose.yml
```
sudo usermod -aG docker $(whoami)
```
In between restart docker daemon
```
docker-compose up -d
```

If you want to be able to work with multiple people on one project you might want to consider to set up a shared db between all users or use db dumps from phpmyadmin to put into the ./sql directory when you do `docker-compose` up to sync between multiple db's (file in that directory have to have '.sql' extension to be automatically imported into db). 
