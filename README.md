# ansible-pglister

Ansible script to install pglister (work in progress)

# Install

```
ansible-galaxy install -r requirements.yml
ansible-galaxy collection install https://gitlab.com/cmatte/ansible-pglister.git
```

# Example playbook

```
---

- hosts: 'yourmachine'
  become: true
  vars:
    le_domains: ['pglister.yourdomain.com']
    domain: 'yourdomain.com'
  roles:
    - role: 'pglister'
      vars:
        service_vhost_name: 'pglister.yourdomain.com'
```

# Authors

- Célestin Matte
- Maxime "pep" Buquet
