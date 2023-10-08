Role Name
=========

ADOTS

Requirements
------------

Setup a dynamic role task file in `<PLAYBOOKDIR>/tasks/__dynamic_role_name.yml` with the content:

```yaml
---
#
- name: "Check for package filter"
  ansible.builtin.set_fact:
    __roles_to_apply: "{{ packages.split(',') | list }}"
  when: packages is defined and packages | length > 0

- name: "{{ ansible_role_name }}: Including adots role "
  ansible.builtin.include_role:
    name: "{{ dotfiles_ng_package | trim }}"
  loop: "{{ __roles_to_apply }}"
  loop_control:
    loop_var: dotfiles_ng_package
```

Role Variables
--------------

%

Dependencies
------------

%

Example Playbook
----------------

```yaml
#
# Usually one entry per 1-X hosts & user.
# - If a host has 5 users that should get setup via this playbook, this should result in 5 entries. 
# - If 5 hosts have one user that should get setup via this playbook, this should result in 1 entry.
#
# -> This makes per user / host entries much simpler and the default paradigm

# user root
- hosts:
    - server
    - server2
  tasks:
    - name: "Adots : {{ remote_user  }} : include backup tasks"
      # This is the task that can call roles based on the host_vars definition
      ansible.builtin.include_tasks:
        file: tasks/__dynamic_role_name.yml
  vars_files:
    - vars/main.yml
  vars:
    # specify user
    ansible_user: root
    #
    # Specify the list of roles (adots-packages) to apply as a list in a variable.
    # Usually one would do that in `host_vars/server.yml`
    # 
    __roles_to_apply: "{{ dotfiles_ng_host_packages }}"
```

# Example adots dotfile package definition

Place the package definition in the roles `defaults/main.yml` file, e.g. `<playbook-dir>/roles/vim/defaults/main.yml`.

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

# Example vim tasks

File: `<PLAYBOOK-DIR>/roles/vim/tasks/main.yml`

```yaml
---
# tasks file for vim

- name: "{{ ansible_role_name }}: Including adots role "
  ansible.builtin.include_role:
    name: adots
    tasks_from: adots.yml
    public: false
```

License
-------

BSD

Author Information
------------------

<sebastian@dystopianfuture.de>
