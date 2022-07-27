## Ansible playbook to boostrap reolink backups

This is a playbook to install [reolink backups](https://github.com/drio/restic-reolink)
on a raspberry pi (or debian linux system).

The playbook takes care of:

* install restic
* instal ftp (vsftpd)
* create reolink user
    * proper directory permissions
    * install script to remove files after x days
    * create subdirectories for the different cameras
    * install cronjob to clean up
* for the pi user:
    * init b2 bucket (maybe run once) — ONLY ONCE (dedicated tag)
    * copy reolink backups repo repo
    * install cron to run backup

TODO/NOTE: Make sure you: 
  - initialize the restic repo before you start doing the backups.
  - setup your cameras do dump videos via ftp on events.
  - make the user dynamic using (pi - drio)
