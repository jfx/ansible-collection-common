# Ansible nginx role

A role to download and install a nginx server.

[![Ansible Galaxy](https://shields.io/badge/Ansible_Galaxy-informational?logo=ansible&style=flat-square)](https://galaxy.ansible.com/jfx/system) Ansible Galaxy collection.

## Getting Started

### Requirements

In order to use:

* Minimal Ansible version: 2.10

### Installation

* Download the `jfx.common` collection:

```shell
ansible-galaxy collection install jfx.common
```

* Then use the role from the collection in the playbook:

example:

```yaml
- hosts: all

  collections:
    - jfx.common

  roles:
    - role: nginx
      vars:
        nginx_sites:
          - my-site
          ...
```

### nginx role variables

* `nginx_sites:`
  * Required - example: `- my-site`
  * Description: List of sites to deploy.

### nginx files

* `nginx-<my-site>.j2`:
A configuration file named `nginx-<my-site>.j2`of a site `my-site` must be located in `{{ playbook_dir }}/templates/` directory.

## Authors

* **FX Soubirou** - *Initial work* - [GitLab repositories](https://gitlab.com/op_so)

## License

This program is free software: you can redistribute it and/or modify it under the terms of the MIT License (MIT). See the [LICENSE](https://opensource.org/licenses/MIT) for details.
