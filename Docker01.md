# COMANDOS DOCKER
## Imagenes

```bash
docker pull

# Retorna todas kas imagenes que se descargo en nuestro pc
docker images
IMAGE   ID             DISK USAGE   CONTENT SIZE   EXTRA

# Descargar imagen en este caso de nodeJS
# 1 Especificas la vercion que se quiero []
# 2 No se especifica y descarga la ultima version [X]
docker pull node 

# Validando una vez descargado
docker images

IMAGE         ID             DISK USAGE   CONTENT SIZE   EXTRA
node:latest   1b84b89ada02        1.8GB          462MB 
#<ETIQUETAS> Puede tener uno o mas
# IMAGES :
# ID: IDENTIFICADOR UNICO
# DISK: DISCO
# USAGE: USO DE ESTACIO
# CONTENT: 
# SIZE
# EXTRA 
# CREATED CUANDO FUE CREADO
-----
# DESCARGANDO UN VERSION ESPECIFICA DE NODEJS
$ docker pull node:22.23.3

# Validamos
IMAGE          ID             DISK USAGE   CONTENT SIZE   EXTRA
node:22.23.3   0e5f90657369       1.65GB          427MB        
node:latest    1b84b89ada02        1.8GB          462MB 
```
> AHORA DESCARGAREMOS  mysql
* [Docker_Mysql](https://hub.docker.com/_/mysql)
```bash
# puedes visitar docker hub y validar cual es el comando inicial
# comando por defaul
docker pull mysql
# comando espesifica la version
docker pull mysql:8.4
# OJO para MAC "procesador m1 apple" si sale error
docker pull --platform linux/x86_64 msql
#validamos
$ docker images
                                                                                                                                                                                                          i IMAGE          ID             DISK USAGE   CONTENT SIZE   EXTRA
mysql:8.4      24989179f588       1.12GB          254MB        
mysql:latest   893418c8a7a3       1.29GB          289MB        
node:22.23.3   0e5f90657369       1.65GB          427MB        
node:latest    1b84b89ada02        1.8GB          462MB  

```
>COMO ELIMINAR IMAGENES
```bash
#indicando version a iliminar
docker image rm node:latest
# validamos
$ docker images
IMAGE          ID             DISK USAGE   CONTENT SIZE   EXTRA
mysql:8.4      24989179f588       1.12GB          254MB        
mysql:latest   893418c8a7a3       1.29GB          289MB        
node:22.23.3   0e5f90657369       1.65GB          427MB  
# al final removemos todo 
docker image rm mysql:8.4
docker image rm msql:latest
```
## COMO CREAR CONTENEDORES
```bash
# Usaremos mongo
docker pull mongo
```
---
Creemos el contenedor
```bash
# Usaremos mongo
docker create mongo
# creo un ID, lo necesitaremos luego
9478c7d9667a6fd29d24e6e8ab625d4812317a051d5a9454f9101d2119fe7607
# Creamos el container
docker container create mongo
# Iniciamos el contenedor usando el ID
docker start 9478c7d9667a6fd29d24e6e8ab625d4812317a051d5a9454f9101d2119fe7607
# validando si docker esta corriendo 
docker ps
CONTAINER ID IMAGE COMMAND                CREATED        STATUS         PORTS       NAMES
9478c7d9667a mongo "docker-entrypoint.s…" 10 minutes ago Up 2 minutes   27017/tcp   competent_shockley
# Detenemos mongo usando el ID corto "9478c7d9667a" 
docker stop 9478c7d9667a
# ver todos los contenedores
$ docker ps -a
CONTAINER ID   IMAGE     COMMAND                  CREATED          STATUS                          PORTS     NAMES
12614d627ecc   mongo     "docker-entrypoint.s…"   8 minutes ago    Created                                   pedantic_hopper
9478c7d9667a   mongo     "docker-entrypoint.s…"   15 minutes ago   Exited (0) About a minute ago             competent_shockley
# Eliminar usando el nombre competent_shockley
docker rm competent_shockley
```
> Creando un nombre al contenedor
```bash
docker create --name monguito mongo
# create : crear 
# --name:
# monguito : el nombre que le estamos poniendo
# mongo : en base a que en este caso en base a mongo

# usamos el nombre para iniciar
$ docker start monguito
monguito

# validamos
$ docker ps -a
CONTAINER ID   IMAGE     COMMAND                  CREATED         STATUS          PORTS       NAMES
9cf2e6794a8b   mongo     "docker-entrypoint.s…"   2 minutes ago   Up 11 seconds   27017/tcp   monguito
```