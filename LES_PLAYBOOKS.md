# Les Playbooks

## Ad-Hoc commande pour afficher les facts 
```ansible target2 -i ../inventory -m setup``

## Les facts dans un fichier YAML
### utilisation de when 
```ansible-playbook -i ../inventory_children ansible_facts_using_when.yml```
### utilisation de la commande assert 
```ansible-playbook -i ../inventory_children ansible_facts_using_assert.yml```  

## Passage d'information entre hosts
## Runtime Inventory 
Pour passer des variables entre remote-to-remote host il est possible
de creer un host de type dummy et lui attacher des variables pour les passer 
vers l'autre host.

```ansible-playbook -i ../inventory_children runtime_inventory_additions.yml```

## Autre exemple avec delegate_to
```ansible-playbook -i ../inventory_children delegate_to_example.yml```

# Utilisation des variables et des filtres 

## Changer the Message Of The Day (MOTD) 
```ansible-playbook -i ../inventory_children motd.yml --limit target2```

## Les filters, creer son propre filtre 
```ansible-playbook -i ../inventory_children new_filter.yml --limit target2```

# Les modules
## Creer son propre module 
Allez dans votre repository github pour creer un token   
clicker sur les Settings de votre compte github et selectionnez  
Developer Settings et ensuite Personnal Access Tokens 
Creer un token et lui donner les droits pour creer un repo github.  
Dans votre home directory faire un ```vi token``` et copier votre
token.  
Toujours sous le prompt venv
faire ```pip3 install requests``` et 
```ansible-playbook -i ../inventory_children ansible_create_module.yml```
# Les Roles

## Mettre le precedement playbook dans un role 
Dans votre home directory toujours sous le prompt venv
faire ```mkdir example-role```  
et ```cd example-role```  
```ansible-galaxy init github.role```  
creer un ficher playbook.yml    
```yaml
- name: use a dedicated Ansible module
  hosts: localhost
  roles:
    - { role: github.role }
```
Dans example-role/github.role/tasks/main.yml 
copier le code suivant
```yaml
# tasks file for github.role
- name: Create a github Repo
  github_repo:
    github_auth_key: "{{ git_key }}"
    name: "repo-create-with-ansible"
    description: "Ansible module for github"
    private: no
    has_issues: no
    has_wiki: no
    has_downloads: no
    state: present
  register: result
```
Dans  example-role/github.role/defaults/main.yml
```yaml
# defaults file for github.role
git_key: d6f90b4be8axxxxxxxxxxxxxxx
```
Revenez dans votre directory ou est installe le playbook et faire
``` ansible-playbook -i ../inventory_children playbook.yml```




































