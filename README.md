# ansible-examples

Demarrer des containers pour simuler plusieurs machines   
``docker run -d --name target1 systemdevformations/ubuntu_ssh
  docker run -d --name target2 systemdevformations/centos_ssh
  docker run -d --name target3 systemdevformations/alpine_ssh``
Retrouver l'adresse ip des containers
Faire un docker ps   

``CONTAINER ID        IMAGE                            COMMAND                  CREATED             STATUS                    PORTS               NAMES
b696423c6b9b        systemdevformations/alpine_ssh   "/entrypoint.sh"         12 minutes ago      Up 12 minutes             22/tcp              target3
  
51d42febdc76        systemdevformations/centos_ssh   "/usr/bin/supervisor…"   12 minutes ago      Up 12 minutes (healthy)   22/tcp              target2
    
4bc05c32d342        systemdevformations/ubuntu_ssh   "/usr/sbin/sshd -D"      13 minutes ago      Up 13 minutes             22/tcp              target1  
``
