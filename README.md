[# Test](https://gitpod.io/workspaces)

# https://github.com/crystalloide/mongoDB

# https://gitpod.io/workspaces

# MongoDB-exemple-with-gitpod

[![Open in Gitpod](https://gitpod.io/button/open-in-gitpod.svg)](https://gitpod.io/#https://github.com/crystalloide/mongoDB)


#	Installez Docker avec Docker Compose V2 en suivant les instructions d’installation ici : https://docs.docker.com/compose/install


https://www.mongodb.com/docs/manual/tutorial/install-mongodb-enterprise-with-docker/

docker pull mongodb/mongodb-enterprise-server:latest


docker run --name mongodb -p 27017:27017 -d mongodb/mongodb-enterprise-server:latest

docker ps -a

wget -qO- https://www.mongodb.org/static/pgp/server-7.0.asc | sudo tee /etc/apt/trusted.gpg.d/server-7.0.asc

sudo apt-get install gnupg

echo "deb [ arch=amd64,arm64 ] https://repo.mongodb.org/apt/ubuntu jammy/mongodb-org/7.0 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-7.0.list

sudo apt-get update

sudo apt-get install -y mongodb-mongosh
sudo apt-get install -y mongodb-org
sudo apt-get install net-tools

mkdir data

## mongod --dbpath /workspace/mongotp/data 
mongod --dbpath /workspace/mongoDB/data 

mongosh

https://27017-crystalloide-mongodb-lygen7vizjf.ws-eu105.gitpod.io/



https://www.mongodb.com/docs/manual/tutorial/install-mongodb-enterprise-with-docker/

