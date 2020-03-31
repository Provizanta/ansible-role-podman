Ansible role: podman
=========

[![Build Status](https://travis-ci.com/Provizanta/ansible-role-podman.svg?branch=master)](https://travis-ci.com/Provizanta/ansible-role-podman)

Establish and configure podman for Linux.

Requirements
------------

None

Role Variables
--------------

These variables are defined in [defaults/main.yml](./defaults/main.yml):


These variables can be specified:

Dependencies
------------

None

Example Playbook
----------------

    - name: Converge
      hosts: all
      roles:
        - role: podman
          vars:

License
-------

MIT

Author Information
------------------

Tibor Csóka
