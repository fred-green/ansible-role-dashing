[![Build Status](https://travis-ci.org/resmo/ansible-role-dashing.svg?branch=master)](https://travis-ci.org/resmo/ansible-role-dashing)

Ansible role for installing Shopify's Dashing dashboard
=======================================================

**ALPHA** This role installs Shopify's' [Dashing](http://shopify.github.io/dashing). It uses NodeJS and installs the ruby environment. After running the playbook, you will find and init script `dashing` to handle dashing as daemon. 

If no dashboard is installed under the `dashing_path`/`dashing_name`, this role will create a new one. If you have an existing dashboard, transfer the files under this path `dashing_path`/`dashing_name`.

The role is installing a init script located in `/etc/init.d/dashing` for handling the daemon.

For testing and development purposes a `Vagrantfile` is available, it uses the same `role.yml` as in Travis CI. So testing this role is just a `vagrant up` away. Then point your browser to http://localhost:8080.

Requirements
------------

Currently only tested and know as working on Ubuntu 12.04. It should work on Debian Wheezy as well, if `wheezy-backports` sources list is available (for installing NodeJS). RHEL 6 support should be available in the near feature.

Role Variables
--------------

* `dashing_pkg_state`:
  - Description: Whether the packages should be just be installed or updated to latest.
  - Values: `installed | latest`
  - Default: `installed`


* `dashing_gem_state`:
  - Description: Whether the gem packages should be just be installed or updated to latest.
  - Values: `present | latest`
  - Default: `present`

* `dashing_service_enable`:
  - Description: Whether the dashing service should be started on boot or not.
  - Values: `yes | no`
  - Default: `yes`

* `dashing_path`:
  - Description: Root path for installing dashboard underneath.
  - Default: `/var/www`

* `dashing_name`:
  - Description: The name of the dashboard directory. Used below `dashing_path`.
  - Default: `dashboard`

* `dashing_address`:
  - Description: Bind to host address
  - Default: `0.0.0.0`

* `dashing_port`:
  - Description: On which port dashing should listen on.
  - Default: `8080`

Dependencies
------------

None.

Example Playbook
-------------------------

    - hosts: dashboard
      roles:
         - { role: resmo.dashing }


    - hosts: dashboard
      roles:
         - { role: resmo.dashing, dashing_port: 80, dashing_path: /srv }

License
-------

BSD

Author Information
------------------

René Moser <mail@renemoser.net>
