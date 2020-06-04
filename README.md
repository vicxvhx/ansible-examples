# Installation du bac a sable ansible-examples

## Mise en place des containers et du fichier inventory
Demarrer des containers pour simuler plusieurs machines.   
```shell script
docker run -d --name target1 systemdevformations/ubuntu_ssh:v2
docker run -d --name target2 systemdevformations/centos_ssh:v4
docker run -d --rm --name target3 --env ROOT_PASSWORD=Passw0rd systemdevformations/alpine-ssh:v1
```
Retrouver le nom des containers  
Faire un docker ps   

```shell script
CONTAINER ID        IMAGE                               COMMAND                  CREATED             STATUS                    PORTS                  NAMES
f5034036dc56        systemdevformations/alpine-ssh:v1   "/entrypoint.sh"         11 hours ago        Up 11 hours               22/tcp                 target3
c714f0b92509        systemdevformations/centos_ssh:v4   "/usr/bin/supervisor…"   23 hours ago        Up 23 hours (unhealthy)   22/tcp                 target2
6051c68c1712        systemdevformations/ubuntu_ssh:v2   "/usr/sbin/sshd -D"      23 hours ago        Up 23 hours               22/tcp                 target1              target1  
```  
 et retrouver l'adresse IP des containers    
 ```shell script
 docker inspect target1 | grep IPAddress  # ubuntu/Passw0rd  
 docker inspect target2 | grep IPAddress  # centos/Passw0rd 
 docker inspect target3 | grep IPAddress  # root/Passw0rd 
```

Depuis la directory /ansible-examples faire ``cp inventory ..``
et modifier le fichier inventory qui a ete copie un niveau au-dessus de l'arborescence  

Avec vi faire des substitions du mot de passe  
```:1,$s/=xxx/<le password prevu pour le cours>/```

en fonction de vos adresses IP fournies pendant le cours   
modifier egalement la VM centos-remote

Dans votre home directory,  faire  
```ssh-keygen -t rsa -b 4096 -C "votre adresse mail"```
Valider les parametres par defaut
sans passphrase  
Et
```ssh-copy-id centos@<remote_id_address>```

## Installation de VirtualEnv Python et faire des Tests avec les Ad-Hoc commandes

Dans votre home directory, faire
`` python3 -m venv venv``  
cela installe le systeme virtualenv Python dans la directory venv  
Faire  
```source venv/bin/activate``` 
Votre prompt change 
```(venv) [centos@ansible-oxiane-controller-2 ~]$```  
Faire   
```pip3 install wheel```
qui install le package wheel qui gere les package Pypi    
et
```pip3 install ansible```

Vous devez egalement installer le package sshpass 
pour utiliser ssh avec un password, c'est-a'dire sans cle ssh.  
```sudo apt-get -y install sshpass```
avec centos
```sudo yum -y install sshpass```


et faire la commande Ansible Ad-Hoc 
```ansible all -m ping -i ../inventory```

Faire ensuite 
``` code 
ansible centos -m yum -a "name=elinks state=latest" -i inventory
ansible centos -b -m yum -a "name=elinks state=latest" -i inventory
ansible centos --list-hosts -i inventory
ansible all -m setup -a "filter=ansible_default_ipv4"  -i inventory
ansible all -m command -a "df -h" -i inventory
ansible centos -b -m yum -a "name=* state=latest" -f 100  -i inventory
ansible centos -m file -a "dest=/home/centos/testfile state=touch" -i inventory 
```
## Presentation des groupes
Dans la directory ansible-examples copiez le fichier inventory children 
vers votre home directory. 
et modifier les passwords et adresses IP comme a l'etape precedente 

## Premier script YAML
Dans la directory ansible-examples editez le fichier ansible_ping.yml
## Premieres commandes ansible-playbook
 ```shell script
ansible-playbook  -i inventory_children ansible_ping.yml  --limit centosdocker
ansible-playbook  -i inventory_children ansible_ping.yml  --limit centos
````