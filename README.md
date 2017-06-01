# Docker Pydio

Docker pydio step by step installation with debian 8 + apache 2 + mysql.

### Español

¿Prefieres leer este README en español?. [Pulsa en este enlace](README_ES.md)

## Prerequisites

- Install [docker engine](https://docs.docker.com/engine/installation/#supported-platforms).
- Install [docker compose](https://docs.docker.com/compose/install/).
- [Create a volume](https://docs.docker.com/engine/tutorials/dockervolumes/#data-volumes)
folder in your home: `mkdir -p ~/.pydio8/html`

## Setup docker image

On the root of this project execute this command:
```shell
docker-compose -f pydio.yml build pydio8
```

If everything is ok, go to next step: [create a container](#create-container).


## Create container

On the root of this project execute this command:
```shell
docker-compose -f pydio.yml up -d pydio8
```

Now execute `docker ps -a` to see all the containers
running or not. If you see "restarting" something was wrong.

If you see "up 4 seconds ago" (or more seconds) go to next step: [Setup database](#setup-database).

## Setup database

I try to keep it simple installing mysql because there is a package on debian with version 5.5 (enought for pydio).

- First, enter inside container: `docker exec -it CONTAINER_ID bash`.

- Install mysql: `apt-get install mysql-server mysql-client`. MySQL will ask you for root user password.

- Create pydio database:
```shell
mysql -h 127.0.0.1 -u root -p
# If you are on localhost, you can avoid "-h 127.0.0.1"
# Now enter your root password.
CREATE DATABASE my_pydio;
\q # quit from mysql shell
```

- If you want, create a custom user for your database. In this tutorial we use root. Don't do that in a production environment!. 


## Pydio setup wizard

Enter in http://localhost:8085/pydio. Select your language and follow the steps (you can ignore warnings right now).
Setup and try the database with your access data.

Host: localhost, user: root (or your custom user), password: your password, database name: my_pydio and try the connection.

If everything is ok, you will see an init tutorial for pydio.

Enjoy!
