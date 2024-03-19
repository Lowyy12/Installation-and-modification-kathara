# Instalación y modificación Kathara
En este repositorio voy a explicar cómo instalar Kathara de una manera fácil y explicar cómo podemos modificar la imagen de otra creando una nueva.

## Clonamos el repositorio

Clonamos el repositorio con el siguiente comando:

````bash
git clone https://github.com/Lowyy12/Installation-and-modification-kathara
````

Le damos permisos de ejecución a install.sh

````bash
chmod +x install.sh
````

````bash
./install.sh
````

Una vez instalado, para que aparezca la imagen del docker tenemos que hacer lo siguiente:

````bash
kathara vstart -n pc1
````
Comando: "docker images"

Resultado:
````
REPOSITORY     TAG       IMAGE ID       CREATED      SIZE

kathara/base   latest    3e7b31aa8be8   5 days ago   1.01GB
````
## Modificando la imagen de arranque
Cambiemos la imagen de la siguiente manera:

````bash
kathara settings

  ║    1 - Choose default manager                                           ║

  ║    2 - Choose default image                                             ║

  ║    3 - Automatically open terminals on startup                          ║

  ║    4 - Choose device shell to be used                                   ║

  ║    5 - Choose terminal emulator to be used                              ║

  ║    6 - Choose Kathara prefixes                                          ║

  ║    7 - Choose logging level to be used                                  ║

  ║    8 - Print Startup Logs on device startup                             ║

  ║    9 - Enable IPv6                                                      ║

  ║   10 - Choose Docker Network Plugin version                             ║

  ║   11 - Automatically mount /hosthome on startup                         ║

  ║   12 - Automatically mount /shared on startup                           ║

  ║   13 - Docker Image Update Policy                                       ║

  ║   14 - Enable Shared Collision Domains                                  ║

  ║   15 - Configure a remote Docker connection                             ║

  ║   16 - Exit                                                             ║
````

Seleccionamos 2
````

  ║    1 - kathara/base                                                     ║

  ║    2 - kathara/bird                                                     ║

  ║    3 - kathara/frr                                                      ║

  ║    4 - kathara/krill                                                    ║

  ║    5 - kathara/openbgpd                                                 ║

  ║    6 - kathara/p4                                                       ║

  ║    7 - kathara/quagga                                                   ║

  ║    8 - kathara/sdn                                                      ║

  ║    9 - Choose another image                                             ║

  ║   10 - Return to Kathara Settings                                       ║
````

Seleccionamos 7

Ejecutamos de nuevo:

````bash
kathara vstart -n pc1
````

Antes de ejecutar kathara wipe, si no lo hemos hecho antes

Result:
````
REPOSITORY       TAG       IMAGE ID       CREATED        SIZE

kathara/base     latest    3e7b31aa8be8   5 days ago     1.01GB
kathara/quagga   latest    62dd101dfa28   5 months ago   1.09GB
````
En nuestro caso vamos
utilizar la imagen de kathara:quagga para instalar vconfig, basándose en la imagen de kathara:quagga,
poniéndole otra etiqueta llamada "vlan".

Vamos a ir a la carpeta Docker que hemos clonado, en la cual hay un documento llamado Dockerfile, si lo leemos podemos ver que estamos instalando sobre la imagen vconf de kathara:quagga, además de actualizar los paquetes.

Haremos el siguiente comando:

````bash
docker build -t kathara/quagga:vlan .
````

Comando:
````bash
docker images
````
Resultado:
````
REPOSITORY       TAG       IMAGE ID       CREATED          SIZE

kathara/quagga   vlan      e78c02b83e3d   22 seconds ago   1.28GB
kathara/base     latest    3e7b31aa8be8   5 days ago       1.01GB
kathara/quagga   latest    62dd101dfa28   5 months ago     1.09GB
````
Ahora solo nos queda cambiar la imagen con la que ejecutamos kathara

## Modificando la imagen de arranque

Lo mismo que habíamos hecho antes:

Comando:
````bash
kathara settings
````
║    2 - Choose default image                                             ║

Seleccionamos 9:

║    9 - Choose another image                                             ║

````bash
Write the name of a Docker image available on Docker Hub (enter q to Quit): kathara/quagga:vlan
````
Ahora si hacemos esto:
````bash
kathara vstart -n pc1
````
Ahora podemos ejecutar vconfig

### Conocimientos usados:

<a href="https://www.gnu.org/software/bash/" target="_blank" rel="noreferrer"> <img src="https://www.vectorlogo.zone/logos/gnu_bash/gnu_bash-icon.svg" alt="bash" width="40" height="40"/> </a>
<a href="https://www.docker.com/" target="_blank" rel="noreferrer"> <img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/docker/docker-original-wordmark.svg" alt="docker" width="40" height="40"/> </a>
