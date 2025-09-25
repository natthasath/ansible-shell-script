# 🎉 Ansible Shell Script

Ansible is an open-source IT automation engine that installs nothing on targets. Define desired state in YAML, then automate provisioning, configuration, app deployment, and orchestration with idempotent playbooks—fast, secure, and agentless at scale.

![version](https://img.shields.io/badge/version-1.0-blue)
![rating](https://img.shields.io/badge/rating-★★★★★-yellow)
![uptime](https://img.shields.io/badge/uptime-100%25-brightgreen)

### ✅ Install Ansible

```shell
sudo apt update

sudo apt install -y python3 python3-venv pipx sshpass

pipx ensurepath

. ~/.profile 2>/dev/null || . ~/.bashrc

export PATH="$PATH:$HOME/.local/bin"
pipx --version
pipx install --include-deps ansible
pipx inject ansible passlib
ansible --version
```

### 🚀 Setup Host & Server

```shell
cp servers.yml.example servers.yml
cp hosts.ini.example host.ini
```

### 🎃 Ansible Ping Check
```shell
cd ~/ansible-lab
ansible local -m ping -o
ansible all -m ping -o
```

```shell
localhost | SUCCESS => {"changed": false, "ping": "pong"}
```

### 🔑 Generate SSH Key on Master Node

```shell
test -f ~/.ssh/id_ed25519 || ssh-keygen -t ed25519 -N "" -f ~/.ssh/id_ed25519
ssh-keygen -lf ~/.ssh/id_ed25519.pub
```

### ©️ Copy to Destination Host

```shell
ssh-copy-id -p 22 admin@10.10.10.10
ssh -p 22 admin@10.10.10.10 'echo OK && hostname && exit'
```

### 🎯 Check Destination Host

```shell
ls -ld ~/.ssh
ls -l ~/.ssh/authorized_keys
tail -n +1 ~/.ssh/authorized_keys
```

### ⚡ Check Server on Ansible Inventory

```shell
ansible-inventory --graph
ansible servers -m ping -o
```

### 🔒 Check Server on Ansible Inventory with Vault

```shell
ansible-vault encrypt group_vars/servers.yml
ansible servers -m ping -o --ask-vault-pass
```

### 🏆 Install Package

```shell
ansible-playbook playbooks/base.yml --tags packages --check
ansible-playbook playbooks/base.yml --tags packages -l prod
ansible-playbook playbooks/base.yml --tags packages -l dev
```

### 🏆 Create User

```shell
ansible-playbook playbooks/user_create.yml -l dev \
  -e create_user_name=username \
  -e create_user_password_plain='changeme'
```

### 🏆 Password User

```shell
ansible-playbook playbooks/user_password.yml -l dev \
  -e target_user=username \
  -e new_password_plain='P@55w0rd' \
  -e force_expire=true \
  -e unlock_account=true
```

### 🏆 Delete User

```shell
ansible-playbook playbooks/user_delete.yml -l dev -e delete_user_name=username
```

### 🏆 Git Pull

```shell
ansible-playbook playbooks/git_pull.yml -l dev \
  -e repo_url=https://github.com/natthasath/ispconfig-shell-script.git \
  -e repo_dest=/home/username/ispconfig-shell-script
```

### 🏆 Disk Report

```shell
ansible-playbook playbooks/disk_report.yml -l dev
```