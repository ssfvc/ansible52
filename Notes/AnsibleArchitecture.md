# Ansible Architecture

![Ansible Architecture](images/ansibleAR.png)


## Ansible core components

* Ad-hoc commands
* Playbooks
* Modules
* Facts
* Inventories
* Variables
* Configuration files
* Templates
* Handlers
* Roles 
* Vault


##  Ad-hoc commands
* An ad-hoc command is something that you might type in to do something really quick, but don’t want to save for later.s
* it is a admin point of view

```
 $ ansible  all -i myhost -b  -m apt -a “name=tree”  
```

## Ansible Playbooks

* Playbook are your instruction manual.
* A playbook is made up with individual plays
* A play is a task
* Play book is in YAML format.

```
---
- hosts: all
  become: yes
  tasks:
  - name:  iam install tree
    apt:
      name: tree
      state: present
  - name:  des install wget
    apt:
      name: wget
      state: present
  - name: des install apache2
    apt:
      name: apache2
      state: present
  - name: des  start apache2 service
    service:
       name: apache2
       state: started
       enabled: yes

```

```
$ ansible-playbook -i myhosts installtree.yml
```

```

PLAY [all] *********************************************************************************

TASK [Gathering Facts] *********************************************************************
ok: [172.31.90.85]

TASK [des i am install git] ****************************************************************
[WARNING]: Could not find aptitude. Using apt-get instead

changed: [172.31.90.85]

TASK [install wget] ************************************************************************
ok: [172.31.90.85]

TASK [install webserver] *******************************************************************
ok: [172.31.90.85]

TASK [start webserver] *********************************************************************
ok: [172.31.90.85]

PLAY RECAP *********************************************************************************
172.31.90.85               : ok=5    changed=1    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0


```
