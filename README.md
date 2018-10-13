# ansible-scaffold

* Use ansible to generate ansible projects and roles.
* Based on [Ansible Best Practices](https://docs.ansible.com/ansible/latest/user_guide/playbooks_best_practices.html).

Why? Becuase I hadnt used ansible in a while and wanted a little refresher.
There are plenty of other ways to acheive the same thing.
e.g. create a git repo that you can just fork


## running


Run `ansible-playbook scaffold.yml` to generate the included example in the `./generated` directory.

```sh
$ ansible-playbook scaffold.yml
```


## customizing


The `scaffold` is configured with a dictionary located in [inventories/local/group_vars/all.yml](./inventories/local/group_vars/all.yml). It has options for the 2 styles of inventories referenced in the best practices.

```yaml
scaffold:
  inventory:
    default: standard
    layouts:
      - standard
      - alternate
```

The `project` is configured with a dictionary locate in [inventories/local/host_vars/localhost](./inventories/local/host_vars/localhost). Multple projects can be described and each project can have multiple roles.

```yaml
projects:
  - name: test-inventory-standard
    basedir: ./generated
    inventory: standard
    roles:
      - common
  - name: test-inventory-alternate
    basedir: ./generated
    inventory: alternate
    roles:
      - common
      - test-role_name
```

You can override the project description by specifying the `extra-vars` option when running the ansible-playbook command. For example, you could run `ansible-playbook scaffold.yml --extra-vars=@myproject.yml` using the following definition in a file named [myproject.yml](./myproject.yml).

```yaml
projects:
  - name: myproject
    basedir: ./generated
    inventory: standard
    roles:
      - mycommonrole
      - myspecialrole
```

