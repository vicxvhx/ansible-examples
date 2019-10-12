# Les Playbooks

## Ad-Hoc commande pour afficher les facts 
```ansible target2 -i ../inventory -m setup``

## Les facts dans un fichier YAML
### utilisation de when 
```ansible-playbook -i ../inventory_children ansible_facts_using_when.yml```
### utilisation de la commande assert 
```ansible-playbook -i ../inventory_children ansible_facts_using_assert.yml```  

## Runtime Inventory 
Pour passer des variables entre remote-to-remote host il est possible
de creer un host de type dummy et lui attacher des variables pour les passer 
vers l'autre host.

```ansible-playbook -i ../inventory_children runtime_inventory_additions.yml```

## Egalement possible de le faire avec delegate_to
```ansible-playbook -i ../inventory_children delegate_to_example.yml```

## Change the Message Of The Day (MOTD) 
```ansible-playbook -i ../inventory_children motd.yml --limit target2```

## Etude sur les filters 
```ansible-playbook -i ../inventory_children new_filter.yml --limit target2```






























