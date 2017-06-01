# Docker Pydio

Docker pydio instalación paso a paso con debian 8 + apache 2 + mysql.

### English

Do you want to read this README in English?. [Click on this link](README.md).

## Prerequisitos

- Instala [docker engine](https://docs.docker.com/engine/installation/#supported-platforms).
- Instala [docker compose](https://docs.docker.com/compose/install/).
- [Crea una carpeta para el volumen](https://docs.docker.com/engine/tutorials/dockervolumes/#data-volumes)
en tu home: `mkdir -p ~/.pydio8/html`

## Configura docker image

En la raíz de este proyecto ejecuta este comando:
```shell
docker-compose -f pydio.yml build pydio8
```

Si todo está ok, vete al siguiente paso: [crea un contenedor](#crea-contenedor).


## Crea contenedor

n la raíz de este proyecto ejecuta este comando:
```shell
docker-compose -f pydio.yml up -d pydio8
```

Ahora ejecuta `docker ps -a` para ver todos los contenedores que están corriendo o no.
Si ves "restarting" algo ha ido mal.

Si ves "up 4 seconds ago" (o más segundos) vete al siguiente paso: [Configurar la base de datos](#configurar-base-de-datos).

## Configurar base de datos

Lo traté de mantener sencillo instalando mysql porque hay un package en debian con la versión 5.5 (suficiente para pydio).

- Primero, entra al contenedor: `docker exec -it CONTAINER_ID bash`.

- Instala mysql: `apt-get install mysql-server mysql-client`. MySQL te preguntará por la contraseña de root.

- Crea la base de datos pydio:
```shell
mysql -h 127.0.0.1 -u root -p
# If you are on localhost, you can avoid "-h 127.0.0.1"
# Now enter your root password.
CREATE DATABASE my_pydio;
\q # quit from mysql shell
```

- Si quieres, crea un usuario personalizado para tu base de datos. En este tutorial usamos root. ¡No hagas esto en un entorno de producción!. 


## Pydio setup wizard

Entra en http://localhost:8085/pydio. Selecciona tu idioma y sigue los pasos (puedes ignorar los warnings por el momento).
Configura y prueba la base de datos con tus datos de acceso.

Host: localhost, user: root (o tu usuario personalizado), password: your password, database name: my_pydio and try the connection.

Si todo está ok, verás el tutorial de inicio de pydio.

A disfrutar!
