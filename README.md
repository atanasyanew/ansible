# Ansible

Home repository of Ansible automation's.

## Installation

1. For windows, install WSL 2
2. Install ansible
   ```bash
   sudo apt install ansible
   ```
3. WSL config to ignore warnings:
   ```bash
   sudo nano /etc/wsl.conf
   ```
   and copy the following content
   ```ini
   [automount]
   enabled = true
   mountFsTab = false
   root = /mnt/
   options = "metadata,umask=22,fmask=11"

   [network]
   generateHosts = true
   generateResolvConf = true
   ```
4. Optional, in order to skip step 3. 
   ```bash
   cd src/
   export ANSIBLE_CONFIG=./ansible.cfg
   ```

## Playbooks

- ``playbooks/octopi.yml``
  Setup Octoprint, update packages, install plugins and restart service.
  ```bash
  ansible-playbook ./playbooks/octopi.yml --ask-pass --ask-become-pass
  ```
- ``playbooks/apt-upgrade.yml``
  apt get and upgrade packages, requires to specify ``hosts``
  ```bash
  # Run against all 
  ansible-playbook ./playbooks/apt-upgrade.yml --ask-pass --ask-become-pass
  # Run just for a few host groups, -k eq --ask-pass
  ansible-playbook ./playbooks/apt-upgrade.yml --limit "octopis,serversGrpSample" -k -K
  # Run for a specific host
  ansible-playbook ./playbooks/apt-upgrade.yml --limit "octopi.local" -k -K
  ```
