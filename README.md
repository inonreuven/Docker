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
3. Running mongoDB and mongo-express countiners in order to make the mongoDB database available to application and also to connect mongo-express to mongoDB countiner:

**- mongoDB and mongo-express connection** - The connection is done with *Isolated Docker Network* which the docker creates to run the countiners. inside the network we can run the mongoDB and mongo-express and the countiners will comunicate with the countiner name. The application outside of the network on the host, will comunicate with the local host port number. 
create docker network named *mongo-network*
```
docker network create mongo-network
```
**- Run mongo countiners**
The ```docker run mongo``` command starts the container from an image. The MongoDB server in the image listens on the standard MongoDB port *27017* inside of a countiner (MongoDB ref) [https://hub.docker.com/_/mongo] and the host will use the same port ```docker run -p -27017:27017 -d```    



