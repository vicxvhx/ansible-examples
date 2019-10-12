# Les Playbooks

## Ad-Hoc commande pour afficher les facts 
```ansible target2 -i ../inventory -m setup``

## Les facts dans un fichier YAML
### utilisation de when 
```ansible-playbook -i ../inventory_children ansible_facts_using_when.yml```
### utilisation de assert 
```ansible-playbook -i ../inventory_children ansible_facts_using_assert.yml```










