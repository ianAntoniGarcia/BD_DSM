# contenedores de sistema gestores de base de datos

## imagene
![ImagenDocker](./img/imahendock.jpg)

> comandos para imagen

- descargar imagenes de postgres

docker pull postgres:14.22-trixie

- Descargar imagen de tutorial de Docker

docker pull docker/getting-started

## Creacion de contenedores

- docker
docker run -d -p 80:80 "Nombre o codigo de la Imagen"

Donde:

- -d detach (background)
- -p puero (el primer numero de puerto no se canbia, el segundo si podemos cambiar)

### Contenedor  de tutorial de Docker
 
docker run -d -p 80:8081 docker/getting-started:latest   
docker run -d -p 80:80 d79336f4812b

### Contenedor de MariaDB sin volumen
docker run -d --name Server-MariadbG1 -p 3343:3306 -e MARIADB_ROOT_PASSWORD=123456 e0236fc6386e

## comandos de docker

| Encabezado 1 | Encabezado 2 |
| :--- | :--- |
| **docker --version** | __Muestra la version del docker__ |
| **docker pull nombre_imagen** | __Descarga una imagen de docker Hub__ [Docker Hub](https://hub.docker.com) |
| **docker images** | __Muestra todas las imagenes__ |
| **docker run** | __crear un contenedor__ |
| **docker ps** | __Visualisa los contenedores que estan en ejecusion__ |
| **docker container ls** | __Visualisa los contenedores que estan en ejecusion__ |
| **docker ps -a** | __Visualisa todos los contenedores__ |
| **docker container ls -a** | __Visualisa todos los contenedores__ |
| **docker rm nombre o ID** | __remover un contenedor__ |
| **docker rm -f nombre o ID** | __Elimina un contenedor que este en ejecusion__ |
