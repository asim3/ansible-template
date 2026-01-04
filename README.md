# Ansible Template


## Setup New AlmaLinux
`ssh-copy-id asim@192.168.122.234`
```bash
sudo useradd --shell /bin/bash --no-log-init --create-home --uid 1234 --groups wheel ansible \
  && sudo mkdir --mode=700 /home/ansible/.ssh \
  && sudo cat ~/.ssh/authorized_keys | sudo tee --append /home/ansible/.ssh/authorized_keys \
  && sudo chown -R ansible:ansible /home/ansible/.ssh \
  && sudo chmod 600 /home/ansible/.ssh/authorized_keys \
  && echo 'ansible ALL=(ALL:ALL) NOPASSWD: ALL' | sudo EDITOR='tee -a' visudo \
  && echo Done
```


## install ansible requirements
```bash
pip install -r requirements.txt

ansible-galaxy collection install ansible.posix community.docker community.general community.postgresql

ansible --version
ansible-community --version
ansible-playbook --version
ansible-galaxy --version
```


## run ansible playbook 
```bash
cd ./src

export ANSIBLE_ROLES_PATH=./roles/v0.1:./roles/v0.2:./roles/v0.3:./roles/v1.0

ansible-playbook -i inventories/development.yml --vault-password-file ${HOME}/.ssh/vault_pass playbooks/setup-docker-station.yml
```


### fix the carriage return control character
```bash
RUN  sed -i -e 's/\r//' ${HOME}/.ssh/*

RUN  sed -i -e 's/\r//' ${HOME}/src/*.*
```
