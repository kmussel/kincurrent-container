#Setting Up Kincurrent with Docker

First download Docker https://docs.docker.com/

Clone this repository.
```bash
git clone git@github.com:kmussel/kincurrent-container.git
git submodule init
git submodule update
```

Setup Orientdb Database
```bash
docker-compose up -d orientdb
```

Go to orientdb in browser {hosturl:2480} 
Create a database using the user "root" and password _0r13ntDB_ or whatever one you set the ORIENTDB_ROOT_PASSWORD env var too.
Create a new user.  This will be the user you set the ORIENTDB_USER and ORIENTDB_PWD environment variables to.

Now that the orient database is setup we can run the next command to set everything else up and start the service.

```bash
docker-compose up -d
```

This will create the containers for the api, orientdb, postgresql, and rabbitmq. 
It will also create a gems data container to keep from having to download all the gems everytime you restart the container.  
It uses volumes to persist the data onto the host for orientdb, postgresql, and rabbitmq.  

Cleanup Commands
```bash
docker rm $(docker ps -a -q)
docker rmi $(docker images | grep “^<none>” | awk '{print $3}')
docker rmi $(docker images | awk '{print $3}'')
```