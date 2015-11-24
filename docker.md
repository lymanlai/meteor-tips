https://www.youtube.com/watch?v=0rQqsvjEeNM

1. docker/1.png

2. https://github.com/gliderlabs/logspout

3. https://github.com/docker/swarm

4. http://kubernetes.io/ Manage a cluster of Linux containers as a single system to accelerate Dev and simplify Ops.

5. http://deis.io/

6. http://paz.sh/

7. https://tutum.co/

8. telescope/dockerfile:  https://github.com/meteorhacks/meteord

9. Meteor up (mupx)

10. BulletProof Meteor: https://goo.gl/O9BJ5g


$(boot2docker shellinit)
netstat -ntpl | grep docker
bash --login '/Applications/Docker/Docker Quickstart Terminal.app/Contents/Resources/Scripts/start.sh'



docker rm -f ping-man
docker run -d --restart=always --name=ping-man ubuntu ping yaha.me
docker run -d --restart:on-failure:10 --name=ping-man ubuntu ping yaha.me
 docker commit `docker ps -lq` lyman/mongo-base
docker run -it lyman/mongo-base /start.sh

### install-mongodb.sh
apt-get update -y
apt-get install wget -y
VERSION=2.6.7
wget https://fastdl.mongodb.org/linux/mongodb-linux-x86_64-$VERSION.tgz -O mongodb.tar.gz
tar xzf mongodb.tar.gz
mv mongodb-linux-x86_64-$VERSION /mongodb
rm mongodb.tar.gz
mkdir -p /data/db

### dockerfile
FROM ubuntu
MAINTAINER Lyman Lai

# install mongodb
COPY install-mongodb.sh /tmp/install-mongodb.sh
RUN /bin/bash /tmp/install-mongodb.sh

ENTRYPOINT /mongodb/bin/mongod

### overwrite default entrypoint
docker run -i -t --entrypoint=/bin/bash lyman/mongo-base2

docker run -d -p 12021:27017 lyman/mongo-base2
