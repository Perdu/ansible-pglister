# Changelog

## 1.0.7

Code cleaning:
- Whole collection is now passing ansible-lint
- Whole collection is now idempotent. Idempotency-related changes:
  - become list user for pip installs to not install as root
  - exim_pglister: only regenerate exim config when necessary
  - exim_pglister: move restart_exim to a handler
  - exim_pglister: fix idempotency in exim.conf editing tasks
  - exim_pglister: override the systemd service file in a proper override file
  - pglister: move tasks to a handler for idempotency
  - make all postgresql_queries idempotent (sometimes with ugly hacks)
  - httpd: fix the lint and idempotency issue related to the rewrite module enabling task
  - add 'creates' for task installing systemd services
  - postgresql: factorize/merge tasks
  - Add hacky workaround to failing idempotency for postgresql_privs tasks
  - pgweb: fix tasks for idempotency
- Set generic organization names in many places
- Some code rewriting for style consistency
- Remove some unnecessary tasks
- Remove useless ignore_errors statements

New features:
- pglister: add possibility to configure links in the banner
- Add http auth when not running in production (adds production option)
  Requires adding variables:
  - http_auth_username
  - http_auth_password
- pgarchives: add pglister address to /etc/hosts to allow local requests without http auth
- http_vhost & httpd: add use_http_auth var, separate from production
- prepare-django-app: now makes a copy of the repository to properly apply changes (for idempotency)

Bugfixes:
- Remove certbot crontab, ensure default certbot systemd timer is enabled instead
- Add default vars to avoid errors
- CI: set production to true to avoid crash
- CI: don't edit /etc/hosts to avoid crash
- prepare_django_app: add handler to restart postgres when necessary
- README: fix molecule command
- Fix pgweb role, which had not been updated to latest changes
- Fix molecule verify command
- httpd: add missing notify

## 1.0.6

New features:
- Replace pglister and pgarchives generic master version with precise commits
- molecule: add MOLECULE_DISTRO variable to image to select image from command line
- Adapt all roles for Debian Bookworm support, drop Debian Buster support
- Update Django roles to Django 4.2
- Bump default postgresql version to 16
- Move django_secret_keys into distinct variables for different roles
- Separate pgarchives django secret key and API secret key
- exim_pglister: add variable exim_log_archive_pipe_output
- pglister & pgarchives: avoid logging password during sites creations to journal
- exim_pglister: don't skip exim.conf configuration when not recreated
- httpd: add option httpd_proxy to activate proxy module
- Let's encrypt: recreate cert when .ini file is deleted
- exim: spamassassin integration: don't scan outgoing emails
- letsencrypt: add a default value for ansible_host (for molecule)
- exim_pglister: enable spamassassin service
- exim_pglister: add exim_log_pglister_pipe_output
- http_vhost: pass user for log creation task (instead of using default 'list' user)
- pglister & pgarchives : factorize repository cloning into prepare_django_app role
- Change default pgarchives version to master
- Install spamd instead of spamassassin for light-weightness- exim_plister: fix tainting issues coming with exim >=4.96
- Add pre_deployment option, to skip some tasks when correct DNS is not set up yet
- let's encrypt: add option to disable certbot internal log rotation mechanism

Bugfixes:
- Let's encrypt: properly verify if cert actually exists
- Code refactoring for ansible-lint
- add tasks to update apt cache instead of doing it in a molecule pretask
- Don't hardcode postresql version
- Don't crash when running pgbackrest check
- Let's encrypt: create directories before everything (+change perms)
- add default value for redeploy
- Use ansible module to properly restart and enable pglister services
- Gitlab-CI related fixes
- apache: give lowest priority to default site
- prepare_django_app: Use ignore_errors to avoid crash when wsgi is already enabled
- make pip packages versions depend on debian version
- httpd: activate proxy module after rewrite to avoid crash

## 1.0.5

- Add files required for ansible-galaxy
- more fixes for ansible-lint

## 1.0.4

- Code refactoring
- Many fixes related to idempotence
