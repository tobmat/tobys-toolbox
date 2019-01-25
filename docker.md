# Docker

**root account**

cd /etc/yum.repos.d/

vi docker.repo

\[dockerrepo\]

name= Docker Repo

baseurl=[https://yum.dockerproject.org/repo/main/centos/7/](https://yum.dockerproject.org/repo/main/centos/7/)

enabled=1

gpgcheck=1

gpgkey=[https://yum.dockerproject.org/gpg](https://yum.dockerproject.org/gpg)

yum update -y

yum install -y docker-engine

systemctl enable docker

systemctl start docker

docker --version

docker images

usermod -a -G docker user

cat /etc/group \| grep docker

yum install elinks -y

**user account**

docker images

docker search centos

docker search nginx

docker search apache

docker pull hello-world

docker run hello-world:latest

docker pull centos:centos6

docker pull centos

docker inspect nginx

docker pull docker/whalesay

docker run docker/whalesay cowsay hello

docker ps

docker ps -a

docker run -it centos:latest /bin/bash

docker run -d centos:latest /bin/bash

docker run -d nginx:latest

docker inspect elated\_austin

elinks [http://172.17.0.2](http://172.17.0.2)

docker stop elated\_austin

docker run -d --name=MyWeb1 nginx:latest

docker stop MyWeb1

docker run -d --name=LifeCycle1 nginx

docker attach LifeCycle1

docker restart LifeCycle1

docker exec -it LifeCycle1 /bin/bash

docker rmi centos:centos6

docker rm stoic\_hamilton

docker rm agitated\_franklin

docker rm $\(docker ps -a -q\)

docker run -d --name=WebServer1 -P nginx

elinks [http://tobmat1.mylabserver.com:32769](http://tobmat1.mylabserver.com:32769)

docker port WebServer1 $CONTAINERREPORT

docker run -d -p 8080:80 --name=WebServer2 nginx

elinks [http://tobmat1.mylabserver.com:8080](http://tobmat1.mylabserver.com:8080)

mkdir www

cd www

vi index.html

docker run -d -p 8080:80 --name=toby -v /home/user/www:/usr/share/nginx/html nginx

mkdir Builds

cd Builds/

docker build -t tobmat123/myapache .

docker run -it tobmat123/myapache /bin/bash

docker build -t tobmat123/myapache .

docker run -d tobmat123/myapache

docker run -d -p 8080:80 --name=toby -v /home/user/www:/usr/share/nginx/html nginx

