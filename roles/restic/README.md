syd.restic
=========

creates a scheduled backup system using [restic](https://restic.readthedocs.io)

Requirements
------------

Requires a systemd system. Installs bash as a requirement. Currently only handles s3 (and compatible) storage.

restic handles deduplication, multiple hosts in the same repository (and deduplication amongst them) and encryption.

Role Variables
--------------

restic_repository:
aws_access_key_id:
aws_secret_access_key:
restic_repository_password:
prune_day:
restic_backup_schedule:
restic_failure_email:
restic_backup_paths:

Dependencies
------------

none

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - name: include syd.restic
      tags: ['always']
      vars:
        restic_repository: s3:s3.us-west-000.backblazeb2.com/repo
        aws_access_key_id: 6tbX0lwepkCL8XeYdXmGkzes
        aws_secret_access_key: aSE8nSGh7kwVSwZcro5mUQW6
        restic_repository_password: "oxhnQfPSTVtVZzhyfoNMhwaX3PDVD9pgI7i9vFCe"
        prune_day: Saturday # pruning operation is expensive, so do it only once a week on this day
        restic_backup_schedule: "*-*-* 05:30:00" # check systemd timer docs for info
        restic_failure_email: email@example.com
        restic_backup_paths:
          - /etc/
          - /var/lib/docker/volumes
      include_role:
        name: syd.restic

License
-------

BSD

Author Information
------------------

Scott Wisely <scott@oneqode.com>
