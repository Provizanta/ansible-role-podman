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

    podman_registries_search: ['docker.io']
    podman_registries_insecure: []
    podman_registries_block: []

These variables can be specified:

    podman_policy:          # dict, YAML to be converted to policy.json content

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
            podman_registries_block:
              - 'registry.fedoraproject.org'
            podman_policy:
              default:
                - type: insecureAcceptAnything
              transports:
                docker-daemon:
                  '':
                    - type: insecureAcceptAnything

License
-------

MIT

Author Information
------------------

Tibor Csóka
