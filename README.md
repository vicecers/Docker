# Docker

### Contruir una imagen

En la raiz del proyecto:

```sh
$ docker build -t {image_name} .
```

En cualquier directorio:

```sh
$ docker build -t {image_name} /path/proyecto
```

### Listar imágenes

```sh
$ docker images
```

### Ejecutar un contenedor en modo desatendido (detached mode) a partir de una imagen

```sh
$ docker run -d -p 85:80 {image_name}
```

### Listar los contenedores que se están ejecutando

```sh
$ docker ps
```

### Ingresar en modo interactivo a un contenedor en ejecución

```sh
$ docker exec -i -t {container_name} /bin/bash
```

### Iniciar una imagen

```sh
$ docker start {container_id}
```

### Detener una imagen

```sh
$ docker stop {container_id}
```

### Eliminar una imagen

```sh
$ docker image rm {image_id}
```

### Eliminar un contenedor

```sh
$ docker rm {container_id}
```

ó

```sh
$ docker container rm {container_id}
```

### Generar un dump de una BD de un container a un directorio local

```sh
$ docker exec {container_id} /usr/bin/mysqldump -u {user} --password={password} {database} > /path/backup.sql
```

Ejemplo:

```sh
$ docker exec 57b3328e0fd3 /usr/bin/mysqldump -u root --password=sql kardex > /Users/andy/Desktop/dump.sql
```

### Restaurar un dump desde un directorio local a una BD de un container

```sh
$ cat backup.sql | docker exec -i {container_id} /usr/bin/mysql -u {user} --password={password} {database}
```

## Comandos de uso frecuente

Para ejecutar los comandos que se mostraran acontinuación es posible que tenga que utilizar "".

**docker version**: El comando "docker --version" muestra la versión de Docker instalada.

```sh
$ docker --version
```

**docker info**: El comando "docker info" muestra la información de todo el sistema docker.

```sh
$ docker info
```

**docker run**: El comando "docker run" nos sirve para crear contenedores y ejecutar comandos dentro de estos.

Ejemplo 1:

```sh
$ docker run hello-world
```

Ejemplo 2:

Ejecutar el comando "ls -l" en un contenedor de la imagen alpine:

```sh
$ docker run alpine ls -l
total 52
drwxr-xr-x    2 root     root          4096 Jul  5 14:47 bin
drwxr-xr-x    5 root     root           340 Aug 12 03:38 dev
drwxr-xr-x    1 root     root          4096 Aug 12 03:38 etc
drwxr-xr-x    2 root     root          4096 Jul  5 14:47 home
drwxr-xr-x    5 root     root          4096 Jul  5 14:47 lib
drwxr-xr-x    5 root     root          4096 Jul  5 14:47 media
drwxr-xr-x    2 root     root          4096 Jul  5 14:47 mnt
dr-xr-xr-x  168 root     root             0 Aug 12 03:38 proc
drwx------    2 root     root          4096 Jul  5 14:47 root
drwxr-xr-x    2 root     root          4096 Jul  5 14:47 run
drwxr-xr-x    2 root     root          4096 Jul  5 14:47 sbin
drwxr-xr-x    2 root     root          4096 Jul  5 14:47 srv
dr-xr-xr-x   13 root     root             0 Aug 12 03:38 sys
drwxrwxrwt    2 root     root          4096 Jul  5 14:47 tmp
drwxr-xr-x    7 root     root          4096 Jul  5 14:47 usr
drwxr-xr-x   11 root     root          4096 Jul  5 14:47 var
```

Ejemplo 3:

Ejecutar el comando "echo" en un contenedor de la imagen alpine:

```sh
$ docker run alpine echo "hello from alpine"
hello from alpine
```

Los comandos anteriores se ejecutan en una instancia de computo.

Ejemplo 4:

Al ejecutar el siguiente comando, el proceso no se va a caer ya que no es un comando de computo volatil.

```sh
$ docker run -it alpine /bin/sh
```

**docker ps**: El comando "docker ps" nos muestra los contenedores que se están ejecutando.

```sh
$ docker ps
```

**docker ps -a**: El comando "docker ps -a" nos muestra todos los contenedores.

```sh
$ docker ps -a
```

**docker search**: El comando docker search nos permite buscar una imagen en Docker Hub, Ejemplos de uso:

Buscar una imagen llamada ubuntu:

```sh
$ docker search ubuntu
```

Buscar una imagen llamada ubuntu y tenga el tag 14.04:

```sh
$ docker search ubuntu:14.04
```

**docker pull**: El comando docker pull nos permite descargar una imagen. Ejemplos de uso:

Sintaxis:

```sh
$ docker pull nombre_imagen
```

Ejemplo:

```sh
$ docker pull alpine
```

Descargar imagen con la última versión de node (latest):

```sh
$ docker pull node
```

Descargar imagen con la versión 8.11.3 de node:

```sh
$ docker pull node:8.11.3
```

**docker images**: El comando docker images nos permite listar todas las imágenes descargadas.

```sh
$ docker images
```

**docker start**: El comando "docker start" permite ejecutar uno o más contenedores detenidos 

Sintaxis:

```sh
$ docker start {container_id}
```

Sintaxis opcional:

```sh
$ docker container start {container_id}
```

Ejemplo:

```sh
$ docker start 1266062bbe0f
```

**docker attach**: El comando "docker attach" permite conectarse a un contenedor. 

```sh
$ docker attach {container_id}
```

```sh
$ docker attach 1266062bbe0f
```

**docker stop**: Este comando nos permite detener un contenedor.

Sintaxis:

```sh
$ docker stop {container_id}
```

ó

```sh
$ docker container stop {container_id}
```

Ejemplo:

```sh
$ docker stop ff33aacf71bd
```

**docker commit**: Este comando nos permite crear una imagen a partir de un contenedor con cambios.

Sintaxis:

```sh
$ docker commit {container_id} {new_name_image}
```

Ejemplo:

```sh
$ docker commit 03224b4dce3e ubuntuejemplo
```

**docker rm**: Este comando nos permite eliminar uno o más contenedores.

```sh
$ docker rm {CONTAINER_ID}
```

## Crear contenedores interactivos

Creamos un nuevo container ejecutando la imagen ubuntu:

```sh
$ docker run -it ubuntu bash
```

El comando anterior ejecutará el container e iniciará sesión en el OS. A continuación saldremos del OS y ejecutaremos docker ps. Podremos ver que no aparece ningún contenedor en ejecución.

```sh
$ exit
$ docker ps

CONTAINER ID        IMAGE                      COMMAND                  CREATED              STATUS                      PORTS 
```

Revisamos el container id:

```sh
$ docker ps -a

CONTAINER ID        IMAGE                      COMMAND                  CREATED              STATUS                       PORTS               NAMES
6d8c807960dc        ubuntu                     "bash"                   About a minute ago   Exited (0) 37 seconds ago
```

Ejecutamos el contenedor creado anteriormente:

```sh
$ docker start 6d8c807960dc
```

En otra terminal podemos ver que el contenedor se lista al ejecutar el comando docker ps

```sh
$ docker ps

CONTAINER ID        IMAGE                      COMMAND                  CREATED              STATUS                       PORTS               NAMES
6d8c807960dc        ubuntu                     "bash"                   About a minute ago   Exited (0) 37 seconds ago
```

Finalmente nos conectamos al contenedor utilizando el comando "docker attach":

```sh
$ docker attach 6d8c807960dc
```

### Salir de un contenedor interactivo sin detenerlo

Para salir de un contenedor interactivo sin detenerlo sólo debemos presionar las teclas ctrl + p + q.

## Iniciar y detener Contenedores en Docker

Vamos a crear un contenedor con la imagen de Ubuntu:

```sh
$ docker run -it ubuntu bash
root@291ab7b22160:/#
```

Ahora vamos a presionar las teclas ctrl + p + q para salir del contenedor sin detenerlo.

A continuación vamos a listar los contenedores que se están ejecutando:

```sh
$ docker ps
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES
291ab7b22160        ubuntu              "bash"              24 seconds ago      Up 23 seconds                           admiring_babbage
```

Vamos a detener el contenedor con el comando "**docker stop**":

```sh
$ docker stop 291
```

Ahora nueevamente listaremos los contenedores que se están ejecutando:

```sh
$ docker ps
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES
```

Como vemos ya esta detenido. Si ingresamos el comando "docker ps -a" veremos el siguiente status "Exited (0) About a minute ago"

```sh
$ docker ps -a
CONTAINER ID        IMAGE                      COMMAND                  CREATED             STATUS                          PORTS               NAMES
291ab7b22160        ubuntu                     "bash"                   4 minutes ago       Exited (0) About a minute ago                       admiring_babbage
```

Ahora vamos a iniciar el contenedor utilizando el comando "**docker start**":

```sh
$ docker start 291
```

Si ingresamos "docker ps" podemos ver que nuevamente tenemos nuestro contenedor ejecutandose:

```sh
$ docker ps
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES
291ab7b22160        ubuntu              "bash"              8 minutes ago       Up 6 seconds                            admiring_babbage
```

Vamos a contectarnos al contenedor utilizando el comando "docker attach":

```sh
$ docker attach 291
root@291ab7b22160:/#
```

## Crear contenedores con nombres

```sh
$ docker run --name prueba -it ubuntu
```

## Crear imagen a partir de contenedor con cambios utilizando Docker Commit

Vamos a crear un contenedor con la imagen de Ubuntu:

```sh
$ docker run -it ubuntu bash
root@03224b4dce3e:/#
```

Crearemos una carpeta llamada jgaitpro y dentro de esta un archivo llamado hola:

```sh
root@03224b4dce3e:/# mkdir jgaitpro
root@03224b4dce3e:/# ls
bin  boot  dev  etc  home  jgaitpro  lib  lib64  media  mkdir  mnt  opt  proc  root  run  sbin  srv  sys  tmp  usr  var
root@03224b4dce3e:/# cd jgaitpro
root@03224b4dce3e:/# touch hola
root@03224b4dce3e:/jgaitpro# ls
hola
```

Ahora vamos a salir del contenedor para crear una imagen a partir de este contenedor. En este ejemplo saldremos del contenedor sin detenerlo (presionando las teclas ctrl + p + q) pero también se puede crear la imagen con el contenedor detenido.

```sh
$ docker ps
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES
03224b4dce3e        ubuntu              "bash"              7 minutes ago       Up 7 minutes                            keen_brown
```

Ahora vamos a crear la imagen utilizando el comando "**docker commit**"

```sh
$ docker commit 03224b4dce3e ubuntujgaitpro
sha256:dcc56f2954c040656460984b5df50754cc18fcba795c78fcf40985bf66b6086b
```

Como podemos ver al ejecutar el comando nos devuelve un sha256. A continuación vamos a listar las imágenes docker: 

```sh
$ docker images
REPOSITORY                 TAG                 IMAGE ID            CREATED             SIZE
ubuntujgaitpro             latest              dcc56f2954c0        24 seconds ago      83.5MB
```

Ahora aparece nuestra imagen creada.

Lo siguiente que haremos será ejecutar un nuevo contenedor utilizando nuestra imagen recién creada.

```sh
$ docker run -it ubuntujgaitpro
root@f8e0d8494697:/# ls
bin  boot  dev  etc  home  jgaitpro  lib  lib64  media  mkdir  mnt  opt  proc  root  run  sbin  srv  sys  tmp  usr  var
root@f8e0d8494697:/# cd jgaitpro
root@f8e0d8494697:/jgaitpro# ls
hola
root@f8e0d8494697:/jgaitpro#
```

Como se puede apreciar los cambios que realizamos en la imagen original se encuentran en nuestra nueva imagen.

Ahora vamos a instalar un servidor web Apache 2 y vamos a crear una imagen nueva a partir de ese contenedor.

```sh
root@f8e0d8494697:/jgaitpro# apt-get update
Get:1 http://security.ubuntu.com/ubuntu bionic-security InRelease [83.2 kB]
Get:2 http://archive.ubuntu.com/ubuntu bionic InRelease [242 kB]
...
Fetched 25.8 MB in 11s (2455 kB/s)
Reading package lists... Done
```

Ingresamos el comando para instalar apache2:

```sh
root@f8e0d8494697:/jgaitpro# apt-get install apache2
```

Una vez finalizada la instalación verificamos si el servicio de apache está corriendo, en caso de no ser así iniciamos el servidor.

```sh
root@f8e0d8494697:/jgaitpro# service apache2 status
 * apache2 is not running
root@f8e0d8494697:/jgaitpro# service apache2 start
 * Starting Apache httpd web server apache2                                                                                                                                          AH00558: apache2: Could not reliably determine the server's fully qualified domain name, using 172.17.0.3. Set the 'ServerName' directive globally to suppress this message
 *
root@f8e0d8494697:/jgaitpro# service apache2 status
 * apache2 is running
```

Ahora vamos a salir del contendor y vamos a crear una nueva imagen a partir de este contenedor, pero ahora utilizaremos unos comandos adicionales:

```sh
$ docker commit --change='CMD ["apache2ctl", "-D FOREGROUND"]' -c "EXPOSE 85" f8e0d8494697 apache2
sha256:25960fe9ebc1d538cc0b4f692b3d68809a79f9e3b82ce8c47decd78d0b353720
```

Con el comando anterior creamos nuestra nueva imagen llamada apache2. Si listamos las imágenes debería aparecer al principio:

```sh
$ docker images
REPOSITORY                 TAG                 IMAGE ID            CREATED             SIZE
apache2                    latest              25960fe9ebc1        23 seconds ago      221MB
ubuntujgaitpro             latest              dcc56f2954c0        24 minutes ago      83.5MB
```

A continuación crearemos un nuevo contenedor utilizando la imagen apache2.

```sh
$ docker run -d -p 5000:80 apache2
4f80c2c0c498e0015728eaef7109cb6081ed9b07d32dcdb054b2c303d3371324
```

## Dockerfile

Dockerfile es la forma fácil de crear imágenes personalizadas por medio de un archivo con todos los "ingredientes" que tendrá nuestra imagen

## Ingredientes Dockerfile

**FROM:** Definir una imagen base para crear nuestra nueva imagen con Dockerfile

Ejemplo: FROM ubuntu:16.04

**MANTAINER:** Hace referencia al creador de la receta

Ejemplo: MAINTAINER JGAITPro Soporte@JGAITPro.com

**RUN:** Nos permite ejecutar comandos en la imagen base antes de ser creada

Ejemplo: RUN apt-get update && apt-get install apache2

**ADD/COPY:** Nos permite agregar o copiar archivos desde el equipo local a la imagen

Ejemplo: ADD index.html /var/www/html

**EXPOSE:** Nos permite exponer por defecto un puerto para el contenedor

Ejemplo: EXPOSE 8080

**CMD:** Ejecutar acción por defecto al crear el contenedor, es la finalidad

Ejemplo: CMD ["/usr/sbin/apache2", "-D", "FOREGROUND"]

## Crear Dockerfiles y construir la app

Vamos a crear una carpeta llamada miweb y dentro de esta un archivo llamado Dockerfile con el siguiente contenido:

```sh
FROM ubuntu:16.04
MAINTAINER ADM
RUN apt-get update
RUN apt-get -y install apache2
EXPOSE 81
CMD /usr/sbin/apache2ctl -D FOREGROUND
```

Una vez hecho esto vamos a realizar el build:

```sh
$ docker build -t miweb /Users/andres/Proyectos/miweb/
```

Al ejecutar el build, podemos los pasos definidos en el archivo Dockerfile se ejecutan en orden, línea por línea. Una vez finalizado si listamos las imágenes aparecerá una nueva imagen llamada "miweb":

```sh
$ docker images
REPOSITORY                 TAG                 IMAGE ID            CREATED             SIZE
miweb                      latest              765a0072c312        2 minutes ago       254MB
```

A continuación vamos a ejecutar un contenedor en modo desatendido (detached mode) a partir de la imagen "miweb":

```sh
$ docker run -d -p 85:80 miweb
2d1cc136f8b92b9b98dc4a66929dc8a4d0039f86905137044e52fdee7a0a3519
```

Podemos verificar con el comando "docker ps" si efectivamente se está ejecutando el contenedor:

```sh
$ docker ps
CONTAINER ID        IMAGE               COMMAND                  CREATED              STATUS              PORTS                        NAMES
2d1cc136f8b9        miweb               "/bin/sh -c '/usr/sb…"   About a minute ago   Up About a minute   81/tcp, 0.0.0.0:85->80/tcp   infallible_spence
```

Podemos ver que efectivamente se está ejecutando el contenedor y esta utilizando el puerto 85 de la máquina anfitrión. Si abrimos un navegador web e ingresamos http://localhost:85/ veremos la página local de apache 2 que nos indica que esta ok. 

Otro ejemplo de Dockerfile:

```sh
FROM ubuntu:16.04
MAINTAINER foo foo@bar.com
RUN apt-get update
RUN apt-get -y install apache2
RUN apt-get -y install wget
RUN apt-get -y install unzip
RUN wget https://github.com/BlackrockDigital/startbootstrap-freelancer/archive/master.zip
RUN unzip master.zip
RUN cp -a /startbootstrap-freelancer-master/* /var/www/html
EXPOSE 82
CMD /usr/sbin/apache2ctl -D FOREGROUND
```

## Docker Mysql:

```sh
$ docker run --name mysql_qa -p 3306:3306 -e MYSQL_ROOT_PASSWORD=root -d mysql
```

Para conectarse desde un cliente utilizar como host localhost / puerto 3306



Links:

- [Docker - Get Started](https://docs.docker.com/get-started/)
- [Hub Docker](https://hub.docker.com/)
- [Forums Docker](https://forums.docker.com/)
- [Docker Compose](https://docs.docker.com/compose/)
- [Get started with Docker Compose](https://docs.docker.com/compose/gettingstarted/)
- [Dockerfile reference](https://docs.docker.com/engine/reference/builder/#usage)
