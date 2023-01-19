Role Name
=========

# Config files

Place config files in one of those folders. They get applied and potentially overwritten in that order,
which allows flexibility and sane defaults

## Universal Config files

Place them in:

- `roles/NAME/files/`

## Distribution specific files

Place them in:

- `roles/NAME/files_os_family/{{ansible_os_family}}/`

## Host specific files

Place them in:

- `roles/NAME/files_hosts/{{ inventory_hostname }}/`


Requirements
------------

Any pre-requisites that may not be covered by Ansible itself or the role should be mentioned here. For instance, if the role uses the EC2 module, it may be a good idea to mention in this section that the boto package is required.

Role Variables
--------------

A description of the settable variables for this role should go here, including any variables that are in defaults/main.yml, vars/main.yml, and any variables that can/should be set via parameters to the role. Any variables that are read from other roles and/or the global scope (ie. hostvars, group vars, etc.) should be mentioned here as well.

Dependencies
------------

A list of other roles hosted on Galaxy should go here, plus any details in regards to parameters that may need to be set for other roles, or variables that are used from other roles.

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - hosts: servers
      roles:
         - { role: username.rolename, x: 42 }


Example adots dotfile package definition
----------------------------------------

Place the package definition in the roles `defaults/main.yml` file.

```yaml
adots:
  name: <NAME> # rolename usually
  type: default
  packages:
    generic: []
    debian:
      - <PACKAGE_NAME_DEBIAN>
    archlinux:
      - <PACKAGE_NAME_ARCH>
    aur: [] # <PACKAGE_NAME_AUR>
    pip: []
  backup_dedicated_only: false
  backup_paths:
    - <PATH/ON/TARGET/HOST>
    - <ANOTHER/PATH/ON/TARGET/HOST>
```

License
-------

BSD

Author Information
------------------

An optional section for the role authors to include contact information, or a website (HTML is not allowed).
