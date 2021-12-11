
# Environnement de production

Environnement de production Docker-Compose pour le projet InfraGame

## Table of Contents

1.  [Description](#Description)
2.  [Docker-compose](#Docker-compose)
3.  [DockerFile](#DockerFile)
4.  [Auteur](#Auteur)
5.  [Version](#Version)

## Description

Environnement de production Docker-Compose pour le projet InfraGame, constitué de 3 container :

  

*  [DB](https://hub.docker.com/_/mysql) : Base de donnée pour nos utilisateurs

*  [Express](https://hub.docker.com/_/node) : Api pour gérer le Back-End de l'appli

*  [React](https://hub.docker.com/_/node) : Framework js pour le Front-End de l'appli

  

## Env Docker

  

### Docker-compose

  

* Le docker compose est sous cette forme

```yml
version:  '3.3'

services:
db:
    container_name:  db
    image:  mysql:5.7
    restart:  always
    environment:
    MYSQL_USER:  'test'
    MYSQL_PASSWORD:  '9908'
    MYSQL_DATABASE:  'infragame'
    MYSQL_ALLOW_EMPTY_PASSWORD:  1
    ports:
    -  3306:3306
    hostname:  mysql

server:
    build:  ./middleware-develop
    container_name:  express
    ports:
    -  5000:5000
    volumes:
    -  ./middleware-develop:/home/node/app/
    command:  npm run start

client:
    build:  ./Interface-develop/
    container_name:  react
    ports:
    -  3000:3000
    volumes:
    -  ./Interface-develop/src:/app/src
    -  ./Interface-develop/public:/app/public
    command:  npm run start -openssl-legacy-provider
```

Il est donc composé des trois containers nommés *db*, *express* et *react* 
|Containers|Ports|
|:--------:|:-------:|
|    DB    |    3306    |
|    React    |    3000    |
|    Express    |    5000   |

### DockerFile

  Les deux Dockerfile sont identique car les deux container react et express sont sous nodeJs
```go
FROM node:16.13
RUN mkdir -p /home/node/app/node_modules
WORKDIR /home/node/app
COPY package*.json ./
RUN npm install
COPY . .
```
### Utilisation

Pour utiliser cet environnement de production il suffit d'injecter les Dockerfile dans leurs dossiers respectifs  
et de lancer le docker-compose comme ceci :
```bash
docker-compose up -d
```

## Auteur

  

Bryan Authiat

Twitter: [@KelBornn](https://twitter.com/kelbornn)

  

## Version

  

* Wait and see for release ;)