# ansible-pglister

Ansible script to install [pglister](https://gitlab.com/pglister/pglister).

Status: the script is finished, but necessary patches are still in the process of being integrated upstream. In the meantime, repositories are still pointing to my own forks. Please use:
- `pgweb_version: 'test'`.
- `pglister_version: 'master'`.
- `pgarchives_version: 'master'`.

# Install

```
ansible-galaxy install -r requirements.yml
ansible-galaxy collection install https://gitlab.com/cmatte/ansible-pglister.git
```

# Example playbook

```
---

- hosts: all
  become: true

  vars_file:
    - vars/defaults.yml

  roles:
    - {role: 'exim_pglister', tags: 'exim_pglister'}
    - {role: 'pglister', tags: 'pglister'}
    - {role: 'pgarchives', tags: 'pgarchives'}
    - {role: 'pgarchives_private', tags: 'pgarchives_private'}
    - {role: 'pgweb', tags: 'pgweb'}

  vars:
    domain: 'yourdomain.com'
    service_vhost_name_pgweb: 'pgweb.yourdomain.com'
    service_vhost_name_pglister: 'pglister.yourdomain.com'
    service_vhost_name_pgarchives: 'pgarchives.yourdomain.com'
    service_vhost_name_pgarchives_private: 'pgarchives-private.yourdomain.com'
    django_superuser_address: "root@yourdomain.com"
    org_name: 'Your organization name'
    use_letsencrypt: true

    # credentials
    database_password: 'CHANGEME'
    django_superuser_pass: 'CHANGEME'
    pgarchives_secret_key: 'CHANGEME'
    recaptcha_site_key: "YOUR_RECAPTCHA_SITE_KEY"  # https://www.google.com/recaptcha/admin/create
    recaptcha_secret_key: "YOUR_RECAPTCHA_SECRET_KEY"
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
