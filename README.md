# ansible-pglister

Ansible script to install [pglister](https://gitlab.com/pglister/pglister).

Status: the script is finished, but necessary patches are still in the process of being integrated upstream. In the meantime, repositories are still pointing to my own forks.

# Install

```
ansible-galaxy install -r requirements.yml
ansible-galaxy collection install https://gitlab.com/cmatte/ansible-pglister.git
```

# Example playbook

```
---

- name: Example playbook
  hosts: all
  become: true

  vars_file:
    - vars/defaults.yml

  roles:
    - {role: 'exim_pglister', tags: 'exim_pglister'}
    - {role: 'pglister', tags: 'pglister'}
    - {role: 'pgarchives', tags: 'pgarchives'}
    - {role: 'pgarchives_private', tags: 'pgarchives_private'}
    - {role: 'pgweb', tags: 'pgweb'}
```

# Redeployment

You can reduce the tasks to repository and related files redeployment using the `redeploy` option, e.g. using `-e "{redeploy: True}"` from the command line.

# Testing

Install the following dependencies:

- molecule
- molecule-plugins
- docker

Then run:
```
molecule test
```

# Authors

- Célestin Matte
- Maxime "pep" Buquet
