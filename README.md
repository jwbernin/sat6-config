Role Name
=========

This role is designed to fully configure a Satellite 6 instance.

The role development was conducted on RHEL 8 against Satellite 6.5.

Requirements
------------

This role requires that the Satellite 6 instance be installed and that a valid
manifest is available. It assumes that the administrator has already run
``satellite-installer'' on the target Satellite but has not performed
any other configuration actions. 

Role Variables
--------------

Variables:

In vault:
satellite_host: FQDN of the Satellite being configured
satellite_user: username of the initial Satellite user (must be an admin)
satellite_password: password for the satellite_user account

Outside vault:
manifest_file: location of the downloaded manifest file on the Ansible control
	node

skip_manifest: if true, skip all actions around uploading a manifest.

repos: list of repositories to enable. Each item should contain a 
	repository label (as name), architecture (as arch), and if
	applicable a release version (as release).

sync_interval: how often the sync will occur (one of "daily", "hourly",
	or "weekly"
sync_date_time: date and time the first scheduled sync should occur.

le_pairs: listing of lifecycle environments and their prior environments.
	Must be in order. Any entry without a 'prior' will use 'Library' as
	the prior.

Dependencies
------------

This role makes use of the foreman-ansible-modules currently under development
at https://github.com/theforeman/foreman-ansible-modules/.

Example Playbook
----------------

Basic usage:

    - hosts: localhost
      roles:
         - sat6-config

We attempt to perform all configuration via the Foreman Ansible modules.

License
-------

GPLv3

Author Information
------------------

Written by John Berninger, john.berninger@redhat.com
