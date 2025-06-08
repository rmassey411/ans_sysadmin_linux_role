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


## Filesystem
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
| filesystem          | N/A                 | dictionary of names, sizes and paths                            |
| directories         | N/A                 | dictionary of paths, user, groups and permissions               |
| N/A                 | N/A                 | N/A                                                             |
| N/A                 | N/A                 | N/A                                                             |
| N/A                 | N/A                 | N/A                                                             |
| N/A                 | N/A                 | N/A                                                             |


Example Playbook
----------------

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
| filesystem          | N/A                 | dictionary of names, sizes and paths                            |
| directories         | N/A                 | dictionary of paths, user, groups and permissions               |
| N/A                 | N/A                 | N/A                                                             |
| N/A                 | N/A                 | N/A                                                             |
| N/A                 | N/A                 | N/A                                                             |
| N/A                 | N/A                 | N/A                                                             |


Example Playbook
----------------

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
