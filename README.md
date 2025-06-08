# ans_linux_misc_role

Manage misc sys admin tasks in linux
- Filesystem
- Packages
- Sudoers
- Users

Requirements
------------

- Linux

Dependencies
------------
- [ansible.posix](https://docs.ansible.com/ansible/latest/collections/ansible/posix/index.html)
- [community.general](https://docs.ansible.com/ansible/latest/collections/community/general/index.html)


## Filesystem
Role Variables
--------------

| Variable            | Choices/Defaults    | Purpose/Description                                             |
| ------------------- | ------------------- | --------------------------------------------------------------- |
| filesystem          | N/A                 | dictionary of names, sizes and paths                            |
| directories         | N/A                 | dictionary of paths, user, groups and permissions               |
| symlinks            | N/A                 | N/A                                                             |


Example Playbook
----------------
How to use role in playbook w/ separate var file

site.yml
  - hosts: servers
    vars_files:
      - filesystem.yml
    roles:
      - ans_linux_filesystem_role

filesystem.yml
  filesystem:
    - name: u01
      size: 10g
      path: "/u01"
  directories:
    - path: "/u01/logs"
      user: "appuser"
      group: "appgroup"
      perms: "0750"
    - path: "/u01/scripts"
      user: "appuser"
      group: "appgroup"
      perms: "0750"


## Packages
Role Variables
--------------

| Variable            | Choices/Defaults    | Purpose/Description                                             |
| ------------------- | ------------------- | --------------------------------------------------------------- |
| packages            | N/A                 | list of packages to be installed                                |

Example Playbook
----------------

```yaml
---
- name: Install packages
  hosts: all #should force host to be specified instead of all keyword so mistake isnt made
  gather_facts: no

  vars:
    packages:
      - podman
      - httpd

  tasks:
    - name: Install packages
      ansible.builtin.include_role:
        name: ans_sysadmin_linux__role
        tasks_from: "packages/pkgs_install.yml"
```

## Patching
Role Variables
--------------

| Variable            | Choices/Defaults    | Purpose/Description                                             |
| ------------------- | ------------------- | --------------------------------------------------------------- |
| filesystem          | N/A                 | dictionary of names, sizes and paths                            |
| directories         | N/A                 | dictionary of paths, user, groups and permissions               |
| N/A                 | N/A                 | N/A                                                             |
| N/A                 | N/A                 | N/A                                                             |
| N/A                 | N/A                 | N/A                                                             |
| N/A                 | N/A                 | N/A                                                             |


Example Playbook
----------------

## Sudoers
Role Variables
--------------

| Variable            | Choices/Defaults    | Purpose/Description                                             |
| ------------------- | ------------------- | --------------------------------------------------------------- |
| group_type          | ad or local         | determine if it's an AD or local group                          |
| managed_by          | central or self     | is the server managed centrally or by the owner                 |
| which_group         | N/A                 | what is the group's name                                        |

Example Playbook
----------------

```yaml
---
- name: Create sudoers file
  hosts: all #should force host to be specified instead of all keyword so mistake isnt made
  gather_facts: no

  vars:
    group_type: "ad"
    managed_by: "self"
    which_group: "dept-team"

  tasks:
    - name: Include role to create sudoers file
      ansible.builtin.include_role:
        name: ans_sysadmin_linux_role
        tasks_from: sudoers/sudoers_create.yml
      vars:
          group_type: ""
          which_group: ""
          managed_by: ""
```


## Users
Role Variables
--------------

| Variable            | Choices/Defaults    | Purpose/Description                                             |
| ------------------- | ------------------- | --------------------------------------------------------------- |
| account_name        | N/A                 | account name                                                    |

Example Playbook
----------------

```yaml
---
- name: Create service account
  hosts: all
  become: yes
  gather_facts: yes

  vars:
    account_name: "app1-mgr"

  tasks:
    - name: Create user
      ansible.builtin.include_role:
        name: ans_sysadmin_linux_role
        tasks_from: "users/svcaccts_create.yml"
      vars:
        account: "{{ account_name }}"

---
- name: Create user account
  hosts: all
  become: yes
  gather_facts: yes

  vars:
    account_name: "user1"

  tasks:
    - name: Create user
      ansible.builtin.include_role:
        name: ans_sysadmin_linux_role
        tasks_from: "users/usraccts_create.yml"
      vars:
        account: "{{ account_name }}"
```