# ansible_masterclass

## csr1000v ssh config

config t
Enter configuration commands, one per line.  End with CNTL/Z.

csr1000v(config)#username admin privilege 15 secret cisco
csr1000v(config)#crypto key generate rsa modulus 2048 general-keys
csr1000v(config)#line vty 0 4
csr1000v(config-line)#login local
csr1000v(config-line)#transport input ssh

csr1000v(config-line)#^Z
csr1000v#copy running-config startup-config

## requirements

Install ubuntu on WSL to run ansible on top and integrate with vscode
Works but is not supported for ansible
VMware player works for images and GNS3 but use hyperV instead
Cisco
Install csr1000v and configure
csr1000v#show ip interface brief
Gets dhcp ip for the interface
Install python3, pip, create virtual env
Install ansible into virtenv
pip install --user ansible-pylibssh

pip install --user ansible-pylibssh

## ecossytem

ansible-pull can pull playbooks from git repo to then run ansible-playbook with them on the inventory
ansible config file, first env var then current dir file (cannot be world writable - security risk)

## commands

```` bash
# change to the python virtual environment
source ~/py_venv/venv1_ansible_latest/bin/activate

# 192.168.1.98 is the csr1000v (with trailing comma)
# note the module cisco and network os of cisco
ansible all -i 192.168.1.98, -c ansible.netcommon.network_cli -u admin -k -m cisco.ios.ios_facts -e ansible_network_os=cisco.ios.ios

# can run arbitrary commands also using the command module with args
ansible all -i 192.168.1.98, -c ansible.netcommon.network_cli -u admin -k -m cisco.ios.ios_command -e ansible_network_os=cisco.ios.ios -a "commands='show ip interface brief'"



````

## inventory

the ansible.cfg can be set to ingore host ssh pub keys host_key_checking=false
