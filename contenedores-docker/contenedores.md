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
docker run -d --name Server-MariadbG1 -p 3343:3306 -e MYSQL_ROOT_PASSWORD=12345 mariadb
 MARIADB_ROOT_PASSWORD=123456 e0236fc6386e
 
 ### Contenedor de MariaDB con volumen

 ···docker
docker volume create v-mariadbg1
docker run -d --name Server-MariadbG1 -p 3343:3306 -e MYSQL_ROOT_PASSWORD=12345  -v v-mariadbg1:/var/lib/mysql mariadb

### Contenedor de postgres con volumen
···Postgres
docker volume create v-postgresG1

docker run -d --name Server-postgresG1 -p 5455:5432 -e POSTGRES_PASSWORD=12345 -v v-postgresG1:/var/lib/postgresql/data postgres

### contenedores de SQLSERVER con volumen

docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<p@ssw0rd>" \
   -p 1450:1433 --name SQLServerG1 \
   -d \
   sha256:d01cc45e6b920eff17abc60295b8748821e09b678f0fcf54959ef37406b80203

v-sqlserverg1
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
| **docker volume ls** | __Mostrar los volumenes que existen en docker__ |


CREATE DATABASE pruebaatributos
CREATE TABLE alumno(
num_alumno int not null PRIMARY KEY,
nombre varchar(50) not null,
apellido_1 varchar(30) not null,
apellido_2 varchar(30) NULL,
fecha_naci date not null
);

INSERT INTO alumono
VALUES (1, "Angel Peres", "Peres", "Hernandes", "1998-09-08");

INSERT INTO alumono
VALUES (2, "Ian Uriel", "Rizo", NULL, "2007-07-25");

SELECT*
FROM alumno;

SELECT NOMBRE, APELLIDO_1, APELLIDO_2 YEAR(fecha_naci),
MONTH(fecha_naci), DAY(fecha_naci),n