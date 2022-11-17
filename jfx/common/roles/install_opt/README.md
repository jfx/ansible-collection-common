# Ansible install opt role

A role to download and install a product in /opt directory.

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

* `io_product`
  * Required - example: `prometheus`
  * Description: Name of th product.
* `io_version`
  * Required - example: `2.40.1`
  * Description: Version of the product.
* `io_package_name`
  * Required - example: `prometheus-2.40.1.linux-amd64`
  * Description: Package name to download without extension.
* `io_package_ext`
  * Default: "" - example: `tar.gz`
  * Description: Define the type of compression. "" for no compression.
* `io_download_link`
  * Required - example: `https://github.com/prometheus/prometheus/releases/download/v2.40.1/{{ io_package_name }}.{{ io_package_ext }}`
  * Description: URL to download product.
* `io_deploy`
  * Default: `true`
  * Description: Creation of 2 links to point to the new version.
* `io_temp_dir_keep`
  * Default: `false`
  * Description: If `true` the temp directory for download is not deleted.

## Authors

* **FX Soubirou** - *Initial work* - [GitLab repositories](https://gitlab.com/op_so)

## License

This program is free software: you can redistribute it and/or modify it under the terms of the MIT License (MIT). See the [LICENSE](https://opensource.org/licenses/MIT) for details.
