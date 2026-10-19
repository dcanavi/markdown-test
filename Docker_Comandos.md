# Guía de comandos Docker

> Referencia práctica para el curso. Los comandos son ejemplos: sustituye `nombre_contenedor`, `nombre_imagen` y otros marcadores por los nombres reales de tu entorno.

## 1. Consultar versiones e información

```bash
# Versión de Docker CLI
docker --version

# Versiones del cliente y del servidor (Engine)
docker version

# Versión de Docker Compose
docker compose version

# Información detallada del entorno Docker
docker info
```

## 2. Descargar imágenes

```bash
# Descargar la etiqueta latest de MySQL
docker pull mysql:latest

# Descargar una versión específica (si la etiqueta existe)
docker pull mysql:8.4.11

# Descargar la rama 8.4; la imagen puede actualizarse dentro de esa rama
docker pull mysql:8.4
```

Consulta las etiquetas disponibles en el registro oficial: <https://hub.docker.com/_/mysql/tags>.

**Nota:** `latest` es una etiqueta móvil. Para reproducir un entorno, fija una etiqueta de versión concreta y verifica que esté disponible.

## 3. Consultar imágenes locales

```bash
# Listar imágenes descargadas
docker images

# Listar imágenes de MySQL
docker images mysql

# Incluir imágenes intermedias
docker images -a
```

## 4. Consultar contenedores y registros

```bash
# Contenedores en ejecución
docker ps

# Todos los contenedores, incluidos los detenidos
docker ps -a

# Uso de recursos en tiempo real
docker stats

# Mostrar los registros de un contenedor
docker logs nombre_contenedor

# Seguir los registros en tiempo real
docker logs -f nombre_contenedor
```

## 5. Crear, iniciar, detener y eliminar contenedores

```bash
# Ejecutar una imagen
docker run nombre_imagen

# Ejecutar en segundo plano
docker run -d nombre_imagen

# Asignar nombre y publicar un puerto del contenedor
# Ejemplo: puerto 8080 del host -> puerto 80 del contenedor
docker run -d --name mi_contenedor -p 8080:80 nombre_imagen

# Detener un contenedor
docker stop nombre_contenedor

# Iniciar un contenedor detenido
docker start nombre_contenedor

# Reiniciar un contenedor
docker restart nombre_contenedor

# Eliminar un contenedor detenido
docker rm nombre_contenedor

# Forzar la eliminación de un contenedor
docker rm -f nombre_contenedor
```

## 6. Volúmenes

```bash
# Crear un volumen
docker volume create n8n_data

# Listar volúmenes
docker volume ls

# Inspeccionar un volumen
docker volume inspect n8n_data

# Eliminar un volumen (solo si ya no contiene datos necesarios)
docker volume rm n8n_data
```

**Precaución:** eliminar un contenedor no equivale a eliminar un volumen. No borres volúmenes que contengan datos que quieras conservar.

## 7. Ejecutar comandos dentro de un contenedor

```bash
# Abrir una shell Bash interactiva (si está instalada en la imagen)
docker exec -it nombre_contenedor bash

# Consultar la versión del cliente MySQL dentro del contenedor
docker exec -it nombre_contenedor mysql --version

# Ejecutar un comando dentro del contenedor
docker exec nombre_contenedor comando
```

Algunas imágenes no incluyen `bash`; en ese caso, prueba `sh` si está disponible.

## 8. Docker Compose

Ejecuta estos comandos desde el directorio que contiene `compose.yaml` o `docker-compose.yml`.

```bash
# Crear e iniciar los servicios
docker compose up

# Iniciar los servicios en segundo plano
docker compose up -d

# Ver el estado de los servicios
docker compose ps

# Mostrar registros de los servicios
docker compose logs

# Seguir los registros en tiempo real
docker compose logs -f

# Construir o reconstruir las imágenes definidas en el archivo
docker compose build

# Detener y eliminar contenedores y redes creados por el proyecto
docker compose down
```

## 9. Comandos vistos en el proyecto de n8n

```bash
# Crear el volumen persistente de n8n
docker volume create n8n_data

# Comprobar la API desde el contenedor n8n
docker compose exec n8n wget -qO- http://sandbox-api:8080/healthz

# Buscar mensajes del runner en los registros de sandbox-api
docker compose logs sandbox-api | grep -i runner

# Comprobar el endpoint de salud de n8n desde el equipo anfitrión
curl -sf http://localhost:5678/healthz
```

El último comando requiere que el servicio publique el puerto `5678` en el equipo anfitrión y que el endpoint de salud esté disponible.

### Ejemplo simplificado de `docker run` para n8n

```bash
docker run -it --rm \
  --name n8n \
  -p 5678:5678 \
  -v n8n_data:/home/node/.n8n \
  n8nio/n8n
```

Este es un ejemplo didáctico. Para un despliegue real, revisa la documentación oficial de n8n y configura de forma segura las variables de entorno, credenciales y persistencia.

## 10. Limpieza y uso de espacio

```bash
# Eliminar imágenes sin uso
docker image prune

# Eliminar contenedores detenidos
docker container prune

# Eliminar redes sin uso
docker network prune

# Limpiar recursos no utilizados
docker system prune

# Consultar el uso de espacio de Docker
docker system df
```

**Precaución:** revisa lo que vas a eliminar antes de confirmar. No uses opciones más agresivas como `--volumes` sin comprobar primero que no borrarás datos necesarios.

## 11. Fuentes oficiales

- Docker CLI: <https://docs.docker.com/reference/cli/docker/>
- Docker Compose: <https://docs.docker.com/compose/>
- Imagen oficial de MySQL y etiquetas: <https://hub.docker.com/_/mysql/tags>
- Imagen oficial de n8n: <https://hub.docker.com/r/n8nio/n8n>

## 12. Plantilla para documentar nuevos comandos

Para cada comando nuevo, registra:

- **Comando:** la instrucción exacta.
- **¿Qué hace?:** una explicación breve.
- **Sintaxis:** qué partes se pueden reemplazar.
- **Ejemplo:** una prueba segura.
- **Resultado esperado:** qué deberías observar.
- **Precauciones:** si puede eliminar datos o cambiar la configuración.
