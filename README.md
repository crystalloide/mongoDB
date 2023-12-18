# MongoDB : installation lancement et utilisation dans gitpod

# https://github.com/crystalloide/mongoDB

# https://gitpod.io/workspaces

[![Open in Gitpod](https://gitpod.io/button/open-in-gitpod.svg)](https://gitpod.io/#https://github.com/crystalloide/mongoDB)


# 1ère façon d'utiliser MongoDB : via docker : 

# https://www.mongodb.com/docs/manual/tutorial/install-mongodb-enterprise-with-docker/

docker pull mongodb/mongodb-enterprise-server:latest


docker run --name mongodb -p 27017:27017 -d mongodb/mongodb-enterprise-server:latest

docker ps -a

Pour arrêter l'instance lancée : 

docker stop mongodb

docker ps -a


# 2nde façon d'utiliser MongoDB : via instalaltion des packages : 

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

test> db.version();
7.0.4

quit

## En adaptant en fonction du nom de votre workspace :  https://27017-crystalloide-mongodb-lygen7vizjf.ws-eu105.gitpod.io/

# Fin du TP
