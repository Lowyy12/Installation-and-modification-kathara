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

We select 2

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
