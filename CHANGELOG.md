# Changelog

## 1.0.6

New features:
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
