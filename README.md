# Docker
 Building docker network with mongo and mongo-express countiners
  
## Contents
1. Objective
2. Step-by-step guide

### 1.Objective

This project aims to provide **step-by-step guide** for docker countiners.

### 2. step-by-step

**1. pulling mongoDB and mongo-express official images** 

1. Use [Docker hub](https://hub.docker.com/search?q=mongo) to search for mongoDB and mongo-express images.
2. pulling the images **command**: 
```docker pull mongo```
and
```docker pull mongo-express```

**2. Running mongoDB and mongo-express countiners** 

Steps to make the mongoDB database available to the application and also to connect mongo-express to mongoDB countiner:  

**- mongoDB and mongo-express connection**

The connection is done with *Isolated Docker Network* which the docker creates to run the countiners. inside the network we can run the mongoDB and mongo-express and the countiners will comunicate with the countiner name. The application outside of the network on the host, will comunicate with the local host port number. 
create docker network named *mongo-network*
```
docker network create mongo-network
```

**- Run mongo countiner**

The ```docker run mongo``` command starts the container from an image. The MongoDB server in the image listens on the standard MongoDB port *27017* inside of a countiner (MongoDB ref) [https://hub.docker.com/_/mongo] and the host will use the same port ```docker run -p 27017:27017 -d```.

- Environment variables:

adjust the initialization of the MongoDB instance by passing one or more environment variables on the ```docker run``` command line
a. setting up the username - ```-e MONGO_INITDB_ROOT_USERNAME=admin```
b. setting up the password - ```-e MONGO_INITDB_ROOT_PASSWORD=password```

the ```-e``` stands for environment variables.
Command syntax:
```docker run -p 27017:27017 -d -e MONGO_INITDB_ROOT_USERNAME=admin -e MONGO_INITDB_ROOT_PASSWORD=password mongo```

- Countiner name and docker network:

Configure the *countiner name* to connect with the mongo express ```--name mongodb``` and the network that we created ```--net mongo-network```.
Command syntax:
```
docker run -p 27017:27017 -d -e MONGO_INITDB_ROOT_USERNAME=admin -e MONGO_INITDB_ROOT_PASSWORD=password --name mongodb --net mongo-network mongo
```

**- Run mongo-express countiner**

To connect the *mongo-express* countainer to the *mongodb* container on startup (mongo-express ref) [https://hub.docker.com/_/mongo-express]:

a. Use the username ```-e ME_CONFIG_MONGODB_ADMINUSERNAME=admin``` and the password of the MongoDB countiner ```-e ME_CONFIG_MONGODB_ADMINPASSWORD=password```

b. Use the MongoDB countainer name to config the server  ```-e ME_CONFIG_MONGODB_SERVER=mongodb``` 

The command syntax:
```
docker run -d^
-p 8081:8081 
-e ME_CONFIG_MONGODB_ADMINUSERNAME=admin^
-e ME_CONFIG_MONGODB_ADMINPASSWORD=password^
-e ME_CONFIG_MONGODB_SERVER=mongodb^
--name mongo-express^ 
--net mongo-network mongo-express^
mongo-express
```












