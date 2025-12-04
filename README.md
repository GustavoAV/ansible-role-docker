# Ansible Role - Docker

Ansible role to setup Docker.

- [Ansible Role - Docker](#ansible-role---docker)
  - [Requirements](#requirements)
  - [Usage](#usage)
  - [Development](#development)
  - [References](#references)

## Requirements

These are the requirements for using this role:

- Operational system: Debian 11+, Ubuntu 22+ or RedHat 9+

## Usage

Create a `requirements.yml` file with the following content

```yaml
---
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
  become: true
  roles: [gustavoav.docker]
```

## Development

> First, install **python3.10** (or higher) and **docker**.

To setup your development environments, run the commands below.

```bash
# Ubuntu/Debian
sudo apt update && sudo apt install -y python3-venv pipx
# RedHat
sudo dnf install -y python3-venv pipx

# Python packages
pipx install --include-deps ansible-dev-tools
pipx inject --include-apps --include-deps ansible-dev-tools $(cat requirements.txt)

pipx ensurepath
source ~/.bashrc
activate-global-python-argcomplete --user

adt --version
molecule --version
```

And then, run this to test everything:

```bash
molecule test
```

## References

- [Docker Docs - Install Docker Engine](https://docs.docker.com/engine/install/)
