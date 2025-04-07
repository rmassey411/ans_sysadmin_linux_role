# ans_linux_misc_role

Setup app volume group and logical volumes with variables file

Requirements
------------

- Linux

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

Dependencies
------------

N/A

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


