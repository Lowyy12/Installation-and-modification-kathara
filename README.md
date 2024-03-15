# Installation-and-modification-kathara
In this repository, I am going to explain how to install Kathara in an easy way and explain how we can modify the image from another by creating a new one.

## We clone the repository

We clone the repository with the following command:

````bash
git clone https://github.com/Lowyy12/Installation-and-modification-kathar
````

We give execution permissions to install.sh

````bash
chmod +x install.sh
````

Once it has been installed, for the docker image to appear we have to do the following:

````bash
kathara vstart -n pc1
````
Comand: "docker images"

Result:
````
REPOSITORY     TAG       IMAGE ID       CREATED      SIZE

kathara/base   latest    3e7b31aa8be8   5 days ago   1.01GB
````
## Modifying boot image
Let's change the image as follows:

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

We select 2
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

We select 7

We execute again:

````bash
kathara vstart -n pc1
````

Before we execute kathara wipe, if we have not done it before

Result:
````
REPOSITORY       TAG       IMAGE ID       CREATED        SIZE

kathara/base     latest    3e7b31aa8be8   5 days ago     1.01GB
kathara/quagga   latest    62dd101dfa28   5 months ago   1.09GB
````
In our case, we are going 
to use the kathara:quagga image to install vconfig, based on the kathara:quagga image, 
putting another tag called "vlan" on it.

We are going to go to the Docker folder that we have cloned, in which there is a document called Dockerfile, if we read it, we can see that we are installing on the kathara:quagga vconf image, in addition to updating the packages.

We will do the following command:

````bash
docker build -t kathara/quagga:vlan .
````

Comand:
````bash
docker images
````
Result:
````
REPOSITORY       TAG       IMAGE ID       CREATED          SIZE

kathara/quagga   vlan      e78c02b83e3d   22 seconds ago   1.28GB
kathara/base     latest    3e7b31aa8be8   5 days ago       1.01GB
kathara/quagga   latest    62dd101dfa28   5 months ago     1.09GB
````
Now we just have to change the image with which we execute kathara

## Modifying boot image

The same way we had done before:

Comand:
````bash
kathara settings
````
║    2 - Choose default image                                             ║

Select 9:

║    9 - Choose another image                                             ║

````bash
Write the name of a Docker image available on Docker Hub (enter q to Quit): kathara/quagga:vlan
````
Now if we do:
````bash
kathara vstart -n pc1
````
We can run vconfig

### Conocimientos usados:

<a href="https://www.gnu.org/software/bash/" target="_blank" rel="noreferrer"> <img src="https://www.vectorlogo.zone/logos/gnu_bash/gnu_bash-icon.svg" alt="bash" width="40" height="40"/> </a>
<a href="https://www.docker.com/" target="_blank" rel="noreferrer"> <img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/docker/docker-original-wordmark.svg" alt="docker" width="40" height="40"/> </a>
