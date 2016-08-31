# Example: Deploy PostgreSQL 9.5

## Server Build

```bash
$ ansible-playbook --inventory=inventory.yml postgres.yml --extra-vars="host=192.168.60.4 user=vagrant"
```

## Create Role

```
ansible --inventory=inventory.yml db \
    --become --become-user=postgres \
    --module-name=postgresql_user \
    --args="name=crunchy password=secret role_attr_flags=CREATEDB,NOSUPERUSER"
```

## Create Database

```
ansible --inventory=inventory.yml db \
    --become --become-user=postgres \
    --module-name=postgresql_db \
    --args="name=crunchy_admin encoding='UTF-8' owner='crunchy'"
```
