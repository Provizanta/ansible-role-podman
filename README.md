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

    podman_registries:          # str, content of the /etc/containers/registry.conf
    podman_registries_conf_d:   # dict, key=file name, value=file content inside /etc/containers/registry.conf.d/
    podman_policy:              # dict, YAML to be converted to 'policy.json' file content
    podman_storage:             # dict, YAML imitating INI like 'storage.conf' file
    podman_seccomp:             # dict, YAML to be converted to 'seccomp.json' file content
    podman_hooks:               # dict, key: hook name, value: YAML to be converted to '*.json' file content

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
            podman_registries: |-
              unqualified-search-registries = ["registry.fedoraproject.org", "registry.access.redhat.com", "docker.io"]

              [[registry]]
              location="localhost:5000"
              insecure=true
            podman_registries_conf_d:
              100-example-blocking.conf: |-
                [[registry]]]
                location="registry.example.org"
                prefix="registry.example.org/example"
                blocked=true
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
