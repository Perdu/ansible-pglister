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
    service_vhost_name_pgweb: 'pgweb.yourdomain.com'
    service_vhost_name_pglister: 'pglister.yourdomain.com'
  roles:
    - role: 'pgweb'
      vars:
        recaptcha_site_key: "YOUR_RECAPTCHA_SITE_KEY" # https://www.google.com/recaptcha/admin/create
        recaptcha_secret_key: "YOUR_RECAPTCHA_SECRET_KEY"
    - role: 'pglister'
      vars:
        pgauth_key: 'YOUR_KEY' # will be generated if not defined
        dc_smarthost: 'smtp.gmail.com::587'
        smtp_relay_password: 'smtp.gmail.com:address@yourdomain.com:YOUR_PASSWORD'
```

# Authors

- Célestin Matte
- Maxime "pep" Buquet
