# Ansible install opt role

A role that downloads and installs a product in /opt directory.

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
    - role: install_opt
      vars:
        io_product: prometheus
        io_version: "{{ prometheus_version }}"
        io_package_name: prometheus-{{ prometheus_version }}.linux-{{ arch }}
        io_package_ext: tar.gz
        io_download_link: https://github.com/prometheus/prometheus/releases/download/v{{ prometheus_version }}/{{ io_package_name }}.{{ io_package_ext }}
```

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

## Authors

* **FX Soubirou** - *Initial work* - [GitLab repositories](https://gitlab.com/op_so)

## License

This program is free software: you can redistribute it and/or modify it under the terms of the MIT License (MIT). See the [LICENSE](https://opensource.org/licenses/MIT) for details.
