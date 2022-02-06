Ansible role: podman
=========

![main Build status](https://github.com/Provizanta/ansible-role-podman/actions/workflows/main.yml/badge.svg)

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

    podman_policy:          # dict, YAML to be converted to 'policy.json' file content
    podman_storage:         # dict, YAML imitating INI like 'storage.conf' file
    podman_seccomp:         # dict, YAML to be converted to 'seccomp.json' file content
    podman_hooks:           # dict, key: hook name, value: YAML to be converted to '*.json' file content

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
            podman_registries_search:
              - 'docker.io'
            podman_policy:
              default:
                - type: insecureAcceptAnything
              transports:
                docker-daemon:
                  '':
                    - type: insecureAcceptAnything
            podman_storage:
              storage:
                driver: "overlay"
                runroot: "/var/run/containers/storage"
                graphroot: "/var/lib/containers/storage"

              storage.options:
                additionalimagestores: []
                size: ""
                override_kernel_check: "true"


License
-------

MIT

Author Information
------------------

Tibor Csóka
