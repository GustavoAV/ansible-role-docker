# Ansible Roles

Ansible roles.

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
