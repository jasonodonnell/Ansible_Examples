## Ansible Modules

Ansible ships with a number of modules (called the ‘module library’) that can be executed directly on remote hosts or through Playbooks.

Users can also write their own modules. These modules can control system resources, like services, packages, or files (anything really), or handle executing system commands.

[Ansible Module Library](http://docs.ansible.com/ansible/modules_by_category.html)

### Example: Install NTP On All Servers

```bash
$ ansible --inventory=inventory.yml multi --sudo \
    --module-name=yum \
    --args="name=ntp state=latest"
```

### Example: Start and Enable NTP On All Servers

```bash
$ ansible --inventory=inventory.yml multi --sudo \
    --module-name=service \
    --args="name=ntpd state=started enabled=yes"
```

### Example: Add bob User To Apps and Add To wheel group

```bash
$ ansible --inventory=inventory.yml app --sudo \
    --module-name=user \
    --args="name=bob uid=1040 groups=wheel"
```

### Example: Create SSH For Bob and Copy To App Servers

First create an SSH key:

```bash
$ ssh-keygen -t rsa -b 4096 -C "test@localhost"
Enter file in which to save the key (~/.ssh/id_rsa): ~/Keys/ansible
```

Next, add the public key to authorized_keys for the user `bob`:

```bash
$ ansible --inventory=inventory.yml app --sudo \
    --module-name=authorized_key \
    --args="user=bob key="{{ lookup('file', '~/keys/ansible.pub') }}"
```

Verify SSH works:

```bash
$ ssh -i ~/keys/ansible bob@192.168.60.5
```
