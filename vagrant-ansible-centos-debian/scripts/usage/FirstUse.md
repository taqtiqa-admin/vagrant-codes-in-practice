#### Tu execute ansible commands under **vagrant** user just create **hosts** file with the following content:
```bash
$ cat hosts
[control]
controller ansible_connection=local

[centos]
centos1 ansible_ssh_pass='freebsd'
centos[2:3] ansible_ssh_user=vagrant ansible_ssh_pass='vagrant' ansible_ssh_port=10022

[debian]
debian[1:3]:10022 ansible_ssh_user=vagrant ansible_ssh_pass='vagrant'

[centos:vars]
ansible_ssh_user=root
ansible_become=true

[debian:vars]
ansible_become=true

[linux:children]
centos
debian

[all:vars]
ansible_ssh_port=10022
```

#### In the same folder will be stored **ansible.cfg** file with the following content: 
```bash
$ cat ansible.cfg
[defaults]
interpreter_python = /usr/bin/python
inventory = hosts
host_key_checking = False
```

#### Check connectivity between hosts for **all** and **linux** group:
```bash
$ ansible all -m ping -o
$ ansible linux -m ping -o
```

#### Look at hosts list:
```bash
$ ansible all --list-hosts
```