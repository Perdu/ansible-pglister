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

- hosts: 'yourmachine'
  become: true
  vars:
    le_domains: ['pglister.yourdomain.com', 'pgweb.yourdomain.com', 'pgarchives.yourdomain.com', 'pgarchives-private.yourdomain.com']
    domain: 'yourdomain.com'
    service_vhost_name_pgweb: 'pgweb.yourdomain.com'
    service_vhost_name_pglister: 'pglister.yourdomain.com'
    service_vhost_name_pgarchives: 'pgarchives.yourdomain.com'
    service_vhost_name_pgarchives_private: 'pgarchives-private.yourdomain.com'
    database_name_pglister: 'pglister'
    database_user: 'list'
    database_password: 'CHANGEME'
    django_superuser_pass: "CHANGEME2"
    django_superuser_address: "root@yourdomain.com"
    base_path_pgweb: '/srv/pgweb'
    base_path_pglister: '/srv/pglister'
    base_path_pgarchives: '/srv/pgarchives'
    base_path_pgarchives_private: '/srv/pgarchives-private'
    cron_emails_destination: 'root'
    org_name: 'Your organization name'  # Name that will be displayed in pglister instead of PostgreSQL
    ip_address_pgweb: '0.0.0.0/0'  # pgweb IP address, to restrict access to the API
    debug: 'False'
    logging_level: 'WARNING'
    # If using an SMTP relay, otherwise leave empty
    # dc_smarthost: 'smtp.gmail.com::587'
    # smtp_relay_password: 'smtp.gmail.com:address@yourdomain.com:YOUR_PASSWORD'
    mailname: 'yourdomain.com'
  roles:
    - role: 'pgweb'
      vars:
        recaptcha_site_key: "YOUR_RECAPTCHA_SITE_KEY" # https://www.google.com/recaptcha/admin/create
        recaptcha_secret_key: "YOUR_RECAPTCHA_SECRET_KEY"
        pgweb_version: '1adaab8955ccf022b1c22b23d62a383854eb0e9e'
        # Example of adding extra vhost definition
        vhost_extra_pglister: |
          Redirect permanent /somewhere https://somewhere_else
    - role: 'pglister'
      vars:
        pgauth_key: 'YOUR_KEY' # will be generated if not defined
        database_name: 'pglister'
        pglister_version: 'master'
        pglister_home_message: '<p><b>To manage your subscriptions, <a href="https://{{ service_vhost_name_pgweb }}/account/signup/">Create an account</a></b></p>'
    - role: 'pgarchives'
      vars:
        database_name: 'pgarchives'
        pgarchives_secret_key: 'CHANGEME3'
        pgarchives_version: 'a4b24b88cb343f778cac5ab66cc6117dac68bf21'
    - role: 'pgarchives-private'
      vars:
        database_name_pgarchives_private: 'pgarchives_private'
```

# Authors

- Célestin Matte
- Maxime "pep" Buquet
