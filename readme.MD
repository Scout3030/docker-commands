
# DOCKER COMMANDS

- Enlaces de interés
[Eliminar imagenes, contenedores y volúmenes](https://www.digitalocean.com/community/tutorials/how-to-remove-docker-images-containers-and-volumes-es#:~:text=Eliminar%20todos%20los%20contenedores%20terminados&text=A%20fin%20de%20revisar%20la,%2Da%20%2Df%20status%3Dexited
)

### Ver imágenes
````
docker images
````
### Descargar imagen con versión específica
````
docker pull image:tag
````
### Filtrar resultados
````
docker images | grep <word>
````
### Eliminar imágenes
````
docker rmi <image>:<tag>
````

### Construir imagen a partir de un dockerfile
````
docker build -t <image-name>:<tag> . 
````

* image-name nombre de la imagen
*  . carpeta donde esta el Dockerfile
* tag opcional, tagear la imagen

### Si el nombre es diferente a Dockerfile

````
docker build -t <image-name>:<tag> -f <docker-file> . 
````
    
### Correr comandos dentro de la imagen 
 (debe contener comando automatizado, sin intervención humana)
````
RUN <command> -y
````
* -y para aceptar el yes que pregunta el comando

### Ver historial de creación de capas de una imagen
````
docker history -H <image-name>:<tag>   
````
* (-H human)

### Definir el CMD
````
CMD apachectl -DFOREGROUND (varia segun imagen)
````

### Construir container a partir de una imagen
````
docker run -d --name <name> <image>
````

### Construir container a partir de una imagen
````
docker run -d --name <name> -p 80:80 <image>
````
* -d: detach mode 
* -p: port 


### copiar todos los archivos del directorio <directory> desde la pc al contenedor
````
copy <directory> /var/www/html 
````

### definir el directorio de trabajo dentro del contenedor
````
WORKDIR /var/www/html
WORKDIR /var/www
````

### Definir variables de entorno
````
ENV <variable> <valor_variable>
RUN echo "$<variable>" > /var/www/html/prueba.html
````

### Exponer puerto
````
EXPOSE <port>
````

### Eliminar el contenedor
````
docker rm -fv <container_id>
````

### Peso de archivo
````
du -sh <file/directory>
````

### crear archivos certificado ssl en local
````
openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout docker.key -out docker.crt
````
* reemplazar docker para construir archivos con nombre diferente

### cambiar nombre de contenedor
````
docker rename <container_name> <container_new_name>
````

### iniciar contenedor
````
docker start <container_name>
````

### reiniciar contenedor
````
docker restart <container_name>
````

### ingresar a contenedor
````
docker exec -it <container_name> bash
````

### ingresar a contenedor como usuario especifico
````
docker exec -u root -it <container_name> bash
````

### listar contenedores unicamentes ids
````
docker ps -q
````

### eliminar todos los contenedores activos
````
docker ps -q | xargs docker rm -f
````

### Eliminarcontainers \<none>

````
docker rmi $(docker images | tail -n +2 | awk '$1 == "<none>" {print $'3'}')
````

### Eliminar todas las imagenes
````
docker rmi $(docker images -q)
````

### Eliminar imagenes y contenedores (en uso y no uso)
````
docker system prune -a
````

### Listar todos los contenedores (incluso los parados)
````
docker ps -a
````

### Eliminar todas las imagenes (incluso los parados)

````
docker stop $(docker ps -a -q)
docker rm $(docker ps -a -q)
````

### crear imagenes con variables de entorno
````
docker run -dit -e "variable=value" --name <container_name> <image>
````

### ver los logs del contenedor
````
docker logs -f <container_id>
````

## LLEGAR AL CONTENEDOR SIN MAPEAR EL PUERTO

### ver información del contenedor
````
docker inspect <container_id>
````

### ingresar por ip (variable)
````
ejem: mysql -u root -h <ip> -p<password>
````

### Ver logs
````
docker logs --tail 50 --follow --timestamps <container_id>
````


## Important commands for node

### Install npm
````
docker run -v "$PWD":/var/www -w /var/www node:14-alpine npm install
````

### npm run dev
````
docker run -v "$PWD":/var/www -w /var/www node:14-alpine npm run dev
````

### npm run watch
````
docker run -v "$PWD":/var/www -w /var/www node:14-alpine npm run watch
````
