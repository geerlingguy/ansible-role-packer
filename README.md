# Ansible Role: Packer

[![Build Status](https://travis-ci.org/geerlingguy/ansible-role-packer.svg?branch=master)](https://travis-ci.org/geerlingguy/ansible-role-packer)

Installs [Packer](https://www.packer.io), a Go-based image and box builder.

## Requirements

None.

## Role Variables

Available variables are listed below, along with default values (see `defaults/main.yml`):

    packer_version: "1.0.0"

The Packer version to install.

    packer_arch: "amd64"

The system architecture (e.g. `386` or `amd64`) to use.

    packer_bin_path: /usr/local/bin

The location where the Packer binary will be installed (should be in system `$PATH`).

    packer_tmp_dir: "/tmp"

The location where the packer archive will be unzipped to.

    packer_force_version: yes

Whether or not packer should update the target machine's `packer` symlink to the
last installed binary.

    packer_purge: no

Whether to remove previous packer versions or not.

## Dependencies

None.

## Example Playbook

    # Install packer using role's defaults (1.0.0)
    - hosts: servers
      roles:
        - geerlingguy.packer

    # Upgrade to a specific version, discarding any  files
    # in `packer_bin_path` matching `packer_*`

    - hosts: servers
      vars:
        packer_version: "1.5.1"
      roles:
        - geerlingguy.packer

    # Downgrade the packer version but keep previous installation(s):

    - hosts: servers
      vars:
        packer_version: "1.4.0"
        packer_purge: no
      roles:
        - geerlingguy.packer

    # Download an additional packer version, but do not
    #  update the default (`{{ packer_bin_path }}/packer`)
    # (implies `packer_purge=no`)
    - hosts: servers
      vars:
        packer_version: "1.2.0"
        packer_update_symlink: no
      roles:
        - geerlingguy.packer

## License

MIT / BSD

## Author Information

This role was created in 2017 by [Jeff Geerling](https://www.jeffgeerling.com/), author of [Ansible for DevOps](https://www.ansiblefordevops.com/).
