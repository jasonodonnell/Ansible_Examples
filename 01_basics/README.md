## Vagrant

Vagrant is software that creates and configures virtual development environments.  It can be seen as a higher-level wrapper around virtualization software such as VirtualBox, VMware, KVM and Linux Containers (LXC), and around configuration management software such as Ansible, Chef, Salt, and Puppet. 

We will use Vagrant to template servers that will run on Virtualbox.  

### Import OS to Vagrant

For the examples we will use CentOS 7 for the servers.  To add the base image of CentOS to Vagrant, issue the following command:

```bash
$ vagrant box add geerlingguy/centos7
```

See the Vagrant website for all the available OS images: https://atlas.hashicorp.com/boxes/search

### Provision Servers

Run the following to provision the servers templated in the `Vagrantfile` in the example directory:

```bash
$ cd 01_basics
$ vagrant up
``` 

## Inventory File

Inventory files are YAML files used to keep track of server inventory by IP or domain-name.  These files can define grouping of servers, embed groups into larger groups and define variables for groups.  

An example inventory file can be found in this directory, defining the servers provisioned by Vagrant/Virtualbox.

## Basic Ansible

With the servers provisioned and the inventory file create, we are ready to issue basic ansible commands against the servers.

### Issue Command To All Servers

```bash
$ ansible --inventory=inventory.yml multi --args="hostname"
```

### Issue Command To App Servers

```bash
$ ansible --inventory=inventory.yml app --args="hostname"
```

### Issue Command To DB Server

```bash
$ ansible --inventory=inventory.yml db --args="hostname"
```
