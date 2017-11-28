# ansible-ocp-kvm
Install OCP on KVM with Ansible
**NOTE** These playbooks are customized for my current environment, thus the lack of customization

## Create cluster:
This playbook will create as many KVM instances as you have defined in the `instances` variable:
```
$ ansible-playbook -i inventories/rromerom playbooks/create-cluster.yml
```

## Prepare hosts
Performs all the steps mentioned in the *Host Preparation* from the official documentation and copies the inventory to the designated host that will perform the installation.
```
$ ansible-playbook -i inventories/apps36 playbooks/prepare-ocp.yml
```
## Install OCP
Now connect to the host you chose to run the playbook and install OCP.
```
$ ssh openshift@master
$ ansible-playbook -i hosts /usr/share/ansible/openshift-ansible/playbooks/byo/openshift-cluster/config.yml
```

## Destroy cluster:
To remove all resources generated, including volumes and /etc/hosts updates
```
$ ansible-playbook -i inventories/rromerom playbooks/destroy-cluster.yml
```
