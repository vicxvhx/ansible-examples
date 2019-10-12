# ansible-examples

## mise en place des containers et de l'inventaire
Demarrer des containers pour simuler plusieurs machines   
``docker run -d --name target1 systemdevformations/ubuntu_ssh
  docker run -d --name target2 systemdevformations/centos_ssh
  docker run -d --name target3 systemdevformations/alpine_ssh``
Retrouver l'adresse ip des containers
Faire un docker ps   

``
CONTAINER ID        IMAGE                            COMMAND                  CREATED             STATUS                    PORTS               NAMES
b696423c6b9b        systemdevformations/alpine_ssh   /entrypoint.sh         12 minutes ago      Up 12 minutes             22/tcp              target3  
51d42febdc76        systemdevformations/centos_ssh   /usr/bin/supervisor…   12 minutes ago      Up 12 minutes (healthy)   22/tcp              target2
4bc05c32d342        systemdevformations/ubuntu_ssh   /usr/sbin/sshd -D     13 minutes ago      Up 13 minutes             22/tcp              target1  
``
 et par container 
  `` docker inspect target1 | grep IPA``
  `` docker inspect target2 | grep IPA``
  `` docker inspect target3 | grep IPA``

Faire un git fork et clone de ce repo  
``git clone  <http votre repo forke>``

Depuis la directory /ansible-examples faire ``cp inventory ..``
et modifier le fichier inventory copie precedement 
en fonction de vos adresses IP  
modifier egalement les groupes de machines centos remote et centos ssh  
 
## Installation de VirtualEnv Python

Dans votre home directory, faire
`` python2 -m venv venv``



