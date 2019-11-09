
# Ansible installation and Configuration:

![ansibleinstall](images/ansibleinstall.jpg)



## stage1 : On Ansible master
```

1) install ansible on ubuntu 16.04
   # apt-add-repository ppa:ansible/ansible
   # sudo apt-get update
   # sudo apt-get install ansible
   # ansible --version

2) create user(maha)
   # addduser maha

3) i want to make (maha) normal user as sudo user.
   # visudo
     maha  ALL=(ALL)   NOPASSWD: ALL
    :wq!
4) for loging into nodes with out pem file
   # vi /etc/ssh/sshd_config
     PasswordAuthentication yes  
     :wq!
   # service ssh restart

my master install has completed.

```
[refer](https://www.digitalocean.com/community/tutorials/how-to-install-and-configure-ansible-on-ubuntu-16-04)

## stage2 : On Ansible Node

```

1) don't install ansible 

2) create user(maha)
   # apt-get update
   # addduser maha

3) i want to make (maha) normal user as sudo user.
   # visudo
     maha  ALL=(ALL)   NOPASSWD: ALL
    :wq!
4) for loging into nodes with out pem file
   # vi /etc/ssh/sshd_config
     PasswordAuthentication yes  
     :wq!
   # service ssh restart

my node config has completed.
```

## Stage3 : On Ansible Master

```
1)  For loging into nodes with out passwd
   $ ssh-keygen  (under maha user)
   $ ssh-copy-id <private ip of ansible node1>
   $ ssh <private ip of node>

2)  ansible way to loging into nodes
   $ mkdir myansible
   $ cd myansible
   $ vi myhosts
     <private ip of all nodes line by line>
     :wq!
   $ ansible all -i myhosts -m ping

3) write a play book and execute.
   vi myping.yml
   ---
   - hosts: all
     become: yes
     tasks:
     - name : i am ping all nodes
       ping:
     - name: install tree
       apt:
        name: tree
    :wq!
   $ ansible-playbook -i myhosts myping.yml



```