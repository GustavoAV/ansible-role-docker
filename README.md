# Ansible Role - Docker <!-- omit from toc -->

Ansible role to setup Docker.

- [Requirements](#requirements)
- [Usage](#usage)
- [Development](#development)
- [References](#references)

## Requirements

These are the requirements for using this role:

- Operational system: Debian 12+, Ubuntu 24+, Fedora 43+, RedHat 9+

## Usage

Create a `requirements.yml` file with the following content

```yaml
---
collections:
  - name: ansible.posix
  - name: community.general

roles:
  - name: gustavoav.docker
    src: git+https://github.com/GustavoAV/ansible-role-docker.git
```

Install the dependencies

```bash
ansible-galaxy install -r requirements.yml
```

Apply the role with a playbook. E.g: Create the following file and apply with `ansible-playbook setup_docker.yml`

```yaml
---
- name: Install Docker
  hosts: all
  roles: [gustavoav.docker]
```

## Development

> First, install [VirtualBox](https://www.virtualbox.org/wiki/Linux_Downloads) and [Vagrant](https://developer.hashicorp.com/vagrant/docs/installation).

Install UV and Ansible

```bash
curl -LsSf https://astral.sh/uv/install.sh | sh
source ~/.local/bin/env

uv tool install ansible-dev-tools --with-executables-from=ansible-core,ansible-lint

# Validation
ansible --version
ansible-lint --version
```

In the `tests/` directory, run the test commands

```bash
cd tests/

make create # Create test VMs
make apply  # Apply Ansible role
make clean  # Remove test VMs

make full   # Runs all the above commands
```

The tests use a **Ubuntu 26.04** image by default. If you want to test with other OSes, run:

```bash
# make <target> BOX=cloud-image/<os>
make full BOX=cloud-image/ubuntu-24.04
```

To test all the possible options

```bash
make full_all
```

## References

- [Docker Docs - Install Docker Engine](https://docs.docker.com/engine/install/)
