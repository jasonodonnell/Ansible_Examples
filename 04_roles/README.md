# Ansible Roles

While it is possible to write a playbook in one very large file (and you might start out learning playbooks this way), eventually you’ll want to reuse files and start to organize things.

At a basic level, including task files allows you to break up bits of configuration policy into smaller files. Task includes pull in tasks from other files. Since handlers are tasks too, you can also include handler files from the ‘handlers:’ section.

See Playbooks if you need a review of these concepts.

Playbooks can also include plays from other playbook files. When that is done, the plays will be inserted into the playbook to form a longer list of plays.

When you start to think about it – tasks, handlers, variables, and so on – begin to form larger concepts. You start to think about modeling what something is, rather than how to make something look like something. It’s no longer “apply this handful of THINGS to these hosts”, you say “these hosts are dbservers” or “these hosts are webservers”. In programming, we might call that “encapsulating” how things work. For instance, you can drive a car without knowing how the engine works.

Roles in Ansible build on the idea of include files and combine them to form clean, reusable abstractions – they allow you to focus more on the big picture and only dive down into the details when needed.

## Example: Provision Lamp Server

```bash
$ vagrant up
$ ansible-playbook --inventory=inventory.yml playbook.yml
```
