# ansible-pglister

Ansible script to install pglister (work in progress)

# Install

```
ansible-galaxy collection install https://gitlab.com/cmatte/ansible-pglister.git
```

# Example playbook

```
---

- hosts: 'yourmachine'
  become: true
  vars:
    le_domains: ['pglister.yourdomain.com']
  roles:
    - role: 'pglister'
      vars:
        service_vhost_name: 'pglister.yourdomain.com'
```
