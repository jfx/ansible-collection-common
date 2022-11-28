# Ansible collection Common

[![Software License](https://img.shields.io/badge/license-MIT-informational.svg?style=flat)](LICENSE)
[![Pipeline Status](https://gitlab.com/op_so/ansible/common/badges/main/pipeline.svg)](https://gitlab.com/op_so/ansible/common/pipelines)
[![semantic-release: angular](https://img.shields.io/badge/semantic--release-angular-e10079?logo=semantic-release)](https://github.com/semantic-release/semantic-release)

An [Ansible](https://www.ansible.com/) collection of common roles for Ubuntu and Debian Operating Systems.

[![GitLab](https://shields.io/badge/Gitlab-informational?logo=gitlab&style=flat-square)](https://gitlab.com/op_so/ansible/common) The main repository.

[![Github](https://shields.io/badge/Github-informational?logo=github&style=flat-square)](https://github.com/jfx/ansible-collection-common) Deployment repository.

[![Ansible Galaxy](https://shields.io/badge/Ansible_Galaxy-informational?logo=ansible&style=flat-square)](https://galaxy.ansible.com/jfx/common) Ansible Galaxy collection.

This collections includes:

| Roles                            | Description                                                     |
| -------------------------------- | --------------------------------------------------------------- |
| [install_opt](#install_opt-role) | A role that downloads and installs a product in /opt directory. |
| [nginx](#nginx-role)             | A role that installs and configures nginx server.               |

## install_opt role

A role that downloads and installs a product in /opt directory with the following structure: `/opt/<product_name>/v<version>/<product_name>`.
Two symlinks are also created, if `io_deploy` variable is `true` (default value):

- `/usr/local/bin/<product_name> -> /opt/<product_name>/current/<product_name>`
- `/opt/<product_name>/current/ -> /opt/<product_name>/v<version>/`

If a new product is deployed (change of `/opt/<product_name>/current/` symlink), the dictionary `io_changed` is returned with a `true` value:
`io_changed: {'<product_name>': true}`
otherwise the value in the dictionary is `false`.

### install_opt role variables

| Variables          | Description                                                                                             | Default      |
| ------------------ | ------------------------------------------------------------------------------------------------------- | ------------ |
| `io_product`       | Name of the product. Example: `prometheus`                                                              | **Required** |
| `io_version`       | Version of the product. Example: `2.40.1`                                                               | **Required** |
| `io_package_name`  | Package name to download without extension. Example: `prometheus-2.40.1.linux-amd64`                    | **Required** |
| `io_package_ext`   | Define the type of compression. "" for no compression. Example: `tar.gz`                                | **Required** |
| `io_download_link` | URL to download product. Example: `https://github.com/ ... /{{ io_package_name }}.{{ io_package_ext }}` | **Required** |
| `io_deploy`        | Creation of 2 links to point to the new version.                                                        | `true`       |
| `io_temp_dir_keep` | If `true` the temp directory for download is not deleted.                                               | `false`      |

### install_opt role output

If a new product is deployed (change of `/opt/<product_name>/current/` symlink), the dictionary `io_changed` is returned with a `true` value:
`io_changed: {'<product_name>': true}`
otherwise the value in the dictionary is `false`.

If a temp directory is created to download the product and `io_temp_dir_keep` is set to `true`, the dictionary `io_temp_dir_path` is returned with the path of the temp directory path:
`io_temp_dir_path: {'<product_name>': '<temp_dir_path>'}`

## nginx role

A role that installs and configures nginx server.

### nginx role variables

| Variables      | Description                                   | Default      |
| -------------- | --------------------------------------------- | ------------ |
| `nginx_sites:` | List of sites to deploy. example: `- my-site` | **Required** |

### nginx files

- `nginx-<my-site>.j2`:
A configuration file named `nginx-<my-site>.j2`of a site `my-site` must be located in `{{ playbook_dir }}/templates/` directory.

## Getting Started

### Requirements

In order to use:

- Minimal Ansible version: 2.10

### Installation

- Download the `jfx.common` collection:

```shell
ansible-galaxy collection install jfx.common
```

- Then use the roles from the collection in the playbook:

example:

```yaml
- hosts: all

  collections:
    - jfx.common

  roles:
    - role: install_opt
      vars:
        io_product: prometheus
        io_version: "{{ prometheus_version }}"
        io_package_name: prometheus-{{ prometheus_version }}.linux-{{ arch }}
        io_package_ext: tar.gz
        io_download_link: https://github.com/prometheus/prometheus/releases/download/v{{ prometheus_version }}/{{ io_package_name }}.{{ io_package_ext }}
        io_deploy: false
        io_temp_dir_keep: true
    - role: nginx
      vars:
        nginx_sites:
          - my-site
          ...
```

## Authors

- **FX Soubirou** - *Initial work* - [GitLab repositories](https://gitlab.com/op_so)

## License

This program is free software: you can redistribute it and/or modify it under the terms of the MIT License (MIT). See the [LICENSE](https://opensource.org/licenses/MIT) for details.
